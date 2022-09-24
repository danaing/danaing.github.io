---
layout: post
title:  "Jupyter Notebook - Cell 줄 바꿈(line wrap) 적용하기"
subtitle: Jupyter Notebook configuration에 line wrap 적용하는 방법
date:   2022-09-24
author: danahkim
categories: Etc.
tags: Jupyter-Notebook
---



주피터 노트북을 html이나 pdf로 변환하여 공유해야할 때가 많다. 셀의 내용이 한 줄에 길 경우 가로로 길게 스크롤을 해야하거나, 아니면 pdf에서 뒷부분이 짤려버린다.

Jupyter notebook의 `nbconfig/notebook.json`에서 몇 가지 설정을 추가해 자동으로 줄바꿈이 되게하는 방법을 소개한다.

먼저 아래 명령어를 통해 jupyter notebook의 configuration 디렉토리를 확인한다. 
```Console
jupyter --config-dir
```
나의 경우는 `/Users/awesome-d/.jupyter` 에 위치한다. 그리고 안에  `nbconfig/notebook.json`가 위치하고 있다.

<img src="/assets/images/Jupyter_Notebook_line_wrap/line_wrap_1.png">

텍스트 편집기를 통해  `nbconfig/notebook.json`에 Code Cell과 Markdown Cell에 줄 바꿈(lineWarpping : true)이 되도록 아래 코드를 추가한다.
```json
{
  "MarkdownCell": {
    "cm_config": {
      "lineWrapping": true
    }
  },
  "CodeCell": {
    "cm_config": {
      "lineWrapping": true
    }
  }
}
```

나의 경우는 아래처럼 추가하였다.

<img src="/assets/images/Jupyter_Notebook_line_wrap/line_wrap_2.png" width=400px>

이제 Jupyer Notebook을 재시작하면 깔끔하게 줄바꿈이 적용된다. 더 이상 셀에 내용이 잘리지 않게 한 화면에 나온다.



## 참고 글
* [python - How to wrap code/text in Jupyter notebooks - Stack Overflow](https://stackoverflow.com/questions/36419342/how-to-wrap-code-text-in-jupyter-notebooks)
