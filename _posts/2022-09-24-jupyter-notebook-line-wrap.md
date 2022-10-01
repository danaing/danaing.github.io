---
layout: post
title:  "Jupyter Notebook - Cell 자동 줄 바꿈(line wrap) 적용하기"
subtitle: Jupyter Notebook configuration에 line wrap 적용하는 방법
date:   2022-09-24
author: danahkim
categories: etc
tags: Jupyter-Notebook
---



Jupyter notebook을 html이나 pdf로 변환하여 공유해야할 때가 많다. 셀의 코드가 한 줄에 길 경우 가로로 길게 스크롤을 해야하거나, 아니면 pdf로 변환했을 때 코드의 뒷부분이 잘려버린다.

Jupyter notebook의 configuration에서 몇 가지 설정으로 자동 줄 바꿈을 적용하는 방법을 소개한다.

먼저 아래 명령어를 통해 jupyter notebook의 configuration 디렉토리를 확인한다.
```Console
$ jupyter --config-dir
```
<img src="/assets/images/Jupyter_Notebook_line_wrap/line_wrap_1.png">

나의 경우는 `/Users/awesome-d/.jupyter` 에 위치한다. 그리고 위에서 확인한 위치 안에 `/nbconfig/notebook.json` 로 이동해서 텍스트 편집기를 통해 Code Cell과 Markdown Cell에 줄 바꿈(lineWrapping : true)이 되도록 아래 코드를 추가한다.

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

이제 Jupyer Notebook을 재시작하면 깔끔하게 줄바꿈이 적용된다.

참고로 pdf로 변환시 주의해야할 점은, jupyter notebook 화면에서 인쇄하기(ctrl+p)를 누른 뒤 인쇄 미리보기 화면 자체를 PDF로 저장해야 코드가 잘리지 않는다.



## 참고 글
* [python - How to wrap code/text in Jupyter notebooks - Stack Overflow](https://stackoverflow.com/questions/36419342/how-to-wrap-code-text-in-jupyter-notebooks)
