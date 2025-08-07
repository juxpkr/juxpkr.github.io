---
layout: archive
title: "Projects: 프로젝트 기록"
permalink: /projects/
header:
  overlay_color: "#333"
  caption: "Azure 클라우드 데이터 엔지니어링 학습"
  entries_layout: grid
---

이 공간은 Azure 클라우드 기반 데이터 엔지니어링 기술을 학습하고 실습하며 기록한 저의 여정입니다.
각 포스팅을 통해 데이터 파이프라인 구축 및 관리에 대한 지식과 경험을 공유합니다.

---

## 모든 프로젝트 포스팅
{% assign posts = site.categories.projects | sort: "date" %}
{% for post in posts %}
	{% include archive-single.html type="grid" %}
{% endfor %}