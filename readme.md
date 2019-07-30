# PATLITE_CTRL

## 概要

シグナルタワー( 3 色表示灯 + ブザー )の制御を  
FANUC ROBOT で行います。

## 使用方法

1. ./KAREL/PATLITE_CTRL.kl を  
   ROBOGUIDE でビルドし、Robot にインポートします。
2. 下記変数を参考にペンダント上で初期設定を行って下さい。  
   (1 度設定を行えばあとは不要です。)

## 変数

### 変数構成

- SETTINGS  
  ├ REGISTER_NO  
  │ └ PATLITE  
  │ 　 └ BUZZER_TIME  
  ├ IO_NO  
  │ └ PATLITE  
  │ 　 ├ PTL_GREEN  
  │ 　 ├ PTL_YELLOW  
  │ 　 ├ PTL_RED  
  │ 　 └ PTL_BUZZER  
  └ FLG_NO  
  　 ├ BUZZER_STOP  
  　 ├ ACTIVE_STAT  
  　 └ PROG_STOP

**_ ※ 変数はペンダント上で変更する必要があります。 _**

### 数値レジスタ番号

1. BUZZER_TIME

### デジタル OUT 番号

1. PTL_GREEN  
   緑点灯 DOUT[x]
2. PTL_YELLOW  
   黄点灯 DOUT[x]
3. PTL_RED  
   赤点灯 DOUT[x]
4. PTL_BUZZER  
   ブザー DOUT[x]

### フラグ番号

1. BUZZER_STOP  
   ブザー停止 FLG[x]
2. ACTIVE_STAT  
   KAREL 実行中ステータス FLG[x]
3. PROG_STOP  
   KAREL 停止 FLG[x]

## 制御条件

基本的な制御条件です。

### 緑灯

- (UOUT[3:Prg running] = ON) AND (UOUT[8:TP enabled] = OFF)  
  点灯
- UOUT[3:Prg running] = OFF  
  消灯

### 黄灯

- (UOUT[3:Prg running] = OFF) AND (UOUT[6:Fault] = OFF) AND (UOUT[7:At perch] = ON)  
  点灯
- ELSE  
  消灯

### 赤灯

- UOUT[6:Fault] = ON  
  点灯
- UOUT[6:Fault] = OFF  
  消灯

### ブザー

- UOUT[6:Fault] = ON(立上がり)  
  動作
- (UOUT[6:Fault] = OFF) or (FLG[SETTINGS.FLG_NO.BUZZER_STOP] = ON)  
  停止

## 更新履歴

## License

Released under the Apache 2.0 License.
