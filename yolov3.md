## YOLO v3を学習

### 必要なもの

- Darknetのインストール
https://github.com/AlexeyAB/darknet

- Yolo3向け初期ウェイトファイル darknet53.conv.74
https://pjreddie.com/media/files/darknet53.conv.74

- Tiny-Yolo3向けウェイトファイル　yolov3-tiny.conv.15
https://pjreddie.com/media/files/yolov3-tiny.weights

### yolo-obj-XXX.cfgファイルの書き換え 
- Batch `batch=64`
- Subdivisions `subdivisions=8`
- `max_batches=classes×2000` if class=3 `max_batches=6000`
- `steps=max_batches×0,8,max_batches×0,9` if max_batches=6000 `steps=4800,5400`
- ３つの[yolo]レイヤーのClasses `classes=3`
- [yolo]レイヤー直前の[convolutional]レイヤーの `filters=(classes+5)×3` if classes=3 `filters=24`


### 学習
学習実行（最初）
```
$ darknet detector train obj.data yolov3-obj-XXX.cfg darknet53.conv.74
```
学習実行（途中から）
```
$ darknet detector train obj.data yolov3-obj-XXX.cfg yolov3-last.weights
```
