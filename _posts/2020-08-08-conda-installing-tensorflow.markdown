---
layout:     notebook
title:      conda로 tensorflow 설치하기 (windows 10)
author:     Soo-young Hwang
tags: 		TIL
subtitle:   TensorFlow Install
category:  study

---


`tensorflow` 입문을 version 1.11.0 으로 했었다.   
그런데 상용화 되어있는 2.x 버전을 사용하는게 맞는 것 같고 자료도 있었기에 업데이트를 했다.   


근데....가상환경을 만들지 않고 `tensorflow`를 설치했었고..  
업데이트하는 과정에서 꼬였다...^^,,,    
왜 `가상환경`을 만들어서 패키지를 임포트해서 쓰라는지 알 것만 같았다(패키지 충돌 방지)....   
그래서 `conda uninstall`하고...(C:\\anaconda3\\uninstall.exe 로 함! 1시간 넘게 걸림)   
다시 [`anaconda`](https://www.anaconda.com/products/individual)를 설치했다.   


#### 목차
- Install TensorFlow 
- Create a Jupyter Notebook Kernel for the TensorFlow Environment


<blockquote>Install TensorFlow</blockquote>

`anaconda` [공식 사이트](https://docs.anaconda.com/anaconda/user-guide/tasks/tensorflow/)에 설치하는 방법을 따라했다.   
1. 아나콘다 혹은 미니콘다를 다운받아 설치한다.   
1. 윈도우 시작메뉴에 있는 Anaconda3 안에 있는`Anaconda Command Prompt`를 실행한다.
1. `tf`와 같은 `TensorFlow` 패키지를 설치할 환경 이름을 고른다. 
1. CPU-only Tensorflow를 설치하려면 

    ```
    conda create -n tf tensorflow
    conda activate tf
    ```
    GPU Tensorflow를 설치하려면
    ```
    conda create -n tf-gpu tensorflow-gpu
    conda activate tf-gpu
    ```

    나는 cpu만 쓰기 때문에 전자로 bash에 입력했다.   

{% highlight bash %}
$ conda create -n tf tensorflow
done
#
# To activate this environment, use
#
#     $ conda activate tf
#
# To deactivate an active environment, use
#
#     $ conda deactivate

{% endhighlight %}   

설치가 완료되면 위에 처럼 done이라고 출력된다.   

{% highlight bash %}
(base) C:\\Users\\Hwang>conda activate tf
(tf) C:\\Users\\Hwang>
{% endhighlight %} 

가상환경이 잘 활성화되는 것도 확인했다.    

`tensorflow`가 잘 임포트되는지 확인했다.   
버전도 함께 확인했다.  

{% highlight bash %}

(tf) C:\\Users\\Hwang>python
Python 3.7.7 (default, May  6 2020, 11:45:54) [MSC v.1916 64 bit (AMD64)] :: Anaconda, Inc. on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> tf.__version__
'2.1.0'
>>>          
{% endhighlight %} 




<blockquote>Create a Jupyter Notebook Kernel for the TensorFlow Environment</blockquote>

그런데 jupyter notebook을 실행해보니 tensorflow 임포트가 안 됐다.   
찾아보니 `TensorFlow` 환경 jupyter notebook kernel을 생성해야했다.   


{% highlight bash %}
(tf) C:\\Users\\Hwang>conda install ipykernel
done
(tf) C:\\Users\\Hwang>python -m ipykernel install --user --name tf --display-name "Tensorflow-CPU"
Installed kernelspec tf in C:\\Users\\Hwang\\AppData\\Roaming\\jupyter\\kernels\\tf
{% endhighlight %} 

`jupyter notebook` 을 bash에 입력하여 실행한 후 파일을 생성하기 위해 `new`키를 누르면 새로운 커널이 생성된 것을 볼 수 있다.   

![1](https://swimmingHwang.github.io/img/jupyter-tensorflow.png)   


<blockquote>
<strong>딥러닝 공부 환경 세팅</strong><br>     
OS :  Windows 10<br>    
python version : 3.7.7<br>    
tensorflow : 2.1.0    
</blockquote>

#### 오늘의 배운점
하라는 대는 다 이유가 있다..   
가상환경을 만들어서 하자...^^,,  
내 시간 ㅠ_ㅠ 하지만 배웠으면 됐지뭐~~~~