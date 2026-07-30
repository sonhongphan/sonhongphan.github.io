---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* Ph.D. Candidate in Computer Vision & AI, Sungkyunkwan University, South Korea (in progress)
  * Advisor: Prof. Jae Wook Jeon
* B.S. in Engineering, <!-- TODO: update with your bachelor's degree, university, and year -->

Research interests
======
* Computer vision for intelligent transportation systems
* Traffic surveillance and vehicle detection under occlusion and adverse weather
* Multi-camera multi-target 3D tracking
* Robust object detection on fisheye cameras

Experience
======
* Present: Graduate Research Assistant
  * Sungkyunkwan University, Suwon, South Korea
  * Research on traffic surveillance benchmarks, 3D tracking, and robust object detection
  * Supervisor: Prof. Jae Wook Jeon

Skills
======
* Python, PyTorch, OpenCV
* Deep learning for object detection and multi-object tracking
* Multi-camera systems and bird's-eye-view (BEV) perception

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
