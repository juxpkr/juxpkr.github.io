---
layout: archive
title: "Learn: 데이터 엔지니어링 학습 기록"
permalink: /learn/
header:
  overlay_color: "#333"
  caption: "Azure 클라우드 데이터 엔지니어링 학습"
---

이 공간은 Azure 클라우드 기반 데이터 엔지니어링 기술을 학습하고 실습하며 기록한 저의 여정입니다.
각 포스팅을 통해 데이터 파이프라인 구축 및 관리에 대한 지식과 경험을 공유합니다.

---

## 모든 학습 포스팅

{% assign posts = site.categories.learn | sort: "date" %}
{% for post in posts %}
	{% include archive-single.html type="grid" %} # 테마 레이아웃에 따라 변경될 수 있음
{% endfor %}