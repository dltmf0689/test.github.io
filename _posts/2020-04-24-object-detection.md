---
title: Object Detection
author: Iseul
layout: post
categories: [Object Detection]
---

## Object Detection  
(객체 검출)

# [Computer Vision]
    객체 검출(Object Detection), 객체 인식(Object Recognition), 객체 추적(Object Tracking) 세 가지 용어가 혼재되어 사용
    Recognition : Object가 어떤 것인지 구분
    Object Detection : Recognition보다 더 작은 범위로써 Object의 존재 유무만 판단

# [Object Detection]

    영상이 들어오면 한 부분에 물체가 있다는걸 인식(Object Recognition)하고, 그 물체가 무엇인지(Object Classification)하고 정확한 위치를 찍어줌(Object Localization)
    Two-shot-detection (초기 버전) : Two-shot이란 2단계를 걸쳐서 검출

    Two-shot-detection (업그레이드 버전) : Regional proposal과 Classification이 순차적으로 이루어짐
    * 영역 제안(Region Proposal)
    객체를 포함할 가능성이 높은 영역을 선택적 탐색(Selective Search)같은 컴퓨터 비전 기술 활용
    딥러닝 기반의 영역 제안 네트워크(RPN; Region Proposal Network)를 통해 선택

    후보군의 윈도우 세트를 취합하면 회귀 모델과 분류 모델의 수를 공식화해 객체 탐지 가능

    (※ Selective Search알고리즘은 Segmentation 분야에 많이 쓰이는 알고리즘이며, 객체와 주변간의 색감(Color), 질감(Texture) 차이, 다른 물체에 애워쌓여있는지(Enclosed) 여부 등을 파악해서 다양한 전략으로 물체의 위치를 파악할 수 있도록 하는 알고리즘
    R-CNN, F-CNN, R-FCN, FPN-FRCN, Fast R-CNN, 등

    * One-shot-detection : Regional proposal과 Classification이 동시에 이루어짐
    input image가 있으면, 하나의 신경망을 통과하여 물체의 bounding box와 class를 동시에 예측
    정해진 위치와 정해진 크기의 객체만 찾음
    위치와 크기들은 대부분의 시나리오에 적용할 수 있도록 전략적으로 선택됨
    보통 원본 이미지를 고정된 사이즈 그리드 영역으로 나눔
    알고리즘은 각 영역에 대해 형태와 크기가 미리 결정된 객체의 고정 개수를 예측
    대표적으로 YOLO, SSD, RetinaNet 등

# [YOLO; You Only Look Once]
    * 대표적인 단일 단계 방식의 객체 탐지 알고리즘
    * 각 이미지를 동일한 크기의 그리드로 나눔
    * 각 그리드에 대해 그리드 중앙을 중심으로 미리 정의된 형태(predefined shape)로 지정된 경계박스 개수를 예측하고 이를 기반으로 신뢰도를 계산
    * 높은 객체 신뢰도를 가진 위치를 선택해 객체 카테고리 파악
    * 객체 포함 여부를 계산하기 위해, 객체 클라스 점수를 계산
    * 이 결과로 총 SxSxN 객체 예측
    * 그리드의 대부분은 낮은 신뢰도를 가짐
    * 신뢰도를 높이기 위해 주변의 그리드를 합칠 수 있음
    * 이후, 임계값을 설정해 불필요한 부분 제거

    * 미리 정의된 형태를 가진 경계박스 수를 '앵커 박스(Anchor Boxes)'라고 함
    * 앵커 박스는 K-평균 알고리즘에 의한 데이터로부터 생성됨, 데이터 세트의 객체 크기와 형태에 대한 사전 정보를 확보

<span class="image center"><img src="{{ 'assets/images/yolo_1.jpeg' | relative_url }}" alt="" /></span>  
