import numpy as np
import cv2

def gamma_tr(x, gamma):
    return pow(x / 255, 1/ ((gamma+1)/100)) * 255
    

cv2.namedWindow('contrast')

cv2.createTrackbar('gamma',
                   'contrast',
                   0, 
                   100,
                   gamma_tr)


cap = cv2.VideoCapture(0)
cap.set(cv2.CAP_PROP_FRAME_WIDTH,  640)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 480)


while(True):

    ret, frame = cap.read()
    if not ret: continue


    v = cv2.getTrackbarPos('gamma',
                           'contrast')
    frame2 = gamma_tr(frame, v)
    cv2.imshow('contrast', frame2)

    k = cv2.waitKey(1)
    if k == ord('q') or k == 27:
        break

cap.release()
cv2.destroyAllWindows()


------------------------
バーを動かすことでガンマの値が変化し、コントラストが変化するような処理を実装した。


<使い方>
上のバーを動かすことでコントラストが変化する。
<依存のライブラリとバージョン>
opencv 3.1.0
numpy 1.14.30


<参考>
1. shuzo kuwako (2015) 【OpenCV】ガンマとシグモイド」, <http://tsukajizo-notes.blogspot.com/2015/11/opencv.html>
   4~5行目の関数に引用。

2. 「宿題２のサンプルコード」, <https://bb9.vle.hiroshima-u.ac.jp/webapps/blackboard/content/listContent.jsp?course_id=_5907_1&content_id=_128168_1>


<実行の様子>
Youtube動画のURL: https://www.youtube.com/channel/UClNhtG4zbLZJyeD9KuHFPbg?view_as=subscribe
