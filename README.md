# peoplesegnet-on-deepstream
peoplesegnet-on-deepstream は、DeepStream 上で PeopleSegNet の AIモデル を動作させるマイクロサービスです。  

## 動作環境
- NVIDIA 
    - DeepStream
- PeopleSegNet
- Docker
- TensorRT Runtime

## PeopleSegNetについて
PeopleSegNet は、画像内の人を検出し、セグメント化されたインスタンスとカテゴリラベルを返すAIモデルです。  
PeopleSegNet は、特徴抽出にResNet50を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順
### Dockerコンテナの起動
Makefile に記載された以下のコマンドにより、PeopleSegNet の Dockerコンテナ を起動します。
```
docker-run: ## Docker ストリーミング用コンテナを建てる
	docker-compose -f docker-compose.yaml up -d
```
### ストリーミングの開始
Makefile に記載された以下のコマンドにより、DeepStream 上の PeopleSegNet でストリーミングを開始します。  
```
stream-start: ## ストリーミングを開始する
	xhost +
	docker exec -it deepstream-peoplesegnet deepstream-app -c /app/src/deepstream_app_source1_peoplesegnet.txt
```
## 相互依存関係にあるマイクロサービス  
本マイクロサービスを実行するために PeopleSegNet の AIモデルを最適化する手順は、[peoplesegnet-on-tao-toolkit](https://github.com/latonaio/peoplesegnet-on-tao-toolkit)を参照してください。  


## engineファイルについて
engineファイルである peoplesegnet.engine は、[peoplesegnet-on-tao-toolkit](https://github.com/latonaio/peoplesegnet-on-tao-toolkit)と共通のファイルであり、当該レポジトリで作成した engineファイルを、本リポジトリで使用しています。  
