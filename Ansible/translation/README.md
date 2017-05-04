Ansible
=======

Ansible is a radically simple IT automation system.  It handles configuration-management, application deployment, cloud provisioning, ad-hoc task-execution, and multinode orchestration - including trivializing things like zero downtime rolling updates with load balancers.

Ansible 은 철저하게 단순한 IT 자동 시스템이다. 앤서블은 설정 관리, 애플리케이션 배포, 클라우드 프로비저닝, ad-hoc 작업 수행, 멀티노드 오케스트레이션 등을 관리한다.

Read the documentation and more at https://ansible.com/
더 자세한 정보 및 문서는 [여기](https://ansible.com/) 에서 찾아볼 수 있다.

Many users run straight from the development branch (it's generally fine to do so), but you might also wish to consume a release.

많은 사람들이 개발 브랜치로 부터 시작하지만(이렇게 해도 일반적으로는 상관없지만), 릴리즈 버전으로부터 시작하는 것을 권장한다.

You can find instructions [here](https://docs.ansible.com/intro_getting_started.html) for a variety of platforms.

자세한 소개문서는 [여기](https://docs.ansible.com/intro_getting_started.html)에있다.

If you want to download a tarball of a release, go to [releases.ansible.com](https://releases.ansible.com/ansible), though most users use `yum` (using the EPEL instructions linked above), `apt` (using the PPA instructions linked above), or `pip install ansible`.

많은 사람들이 `yum`이나 `apt`, `pip`을 이용하여 설치하고 있지만, 만약 릴리즈 버전의 타르볼을 받고 싶으면 [release.ansible.com](https://releases.ansible.com/ansible)에서 받을 수 있다.


Design Principles
디자인 원칙
=================

   * Have a dead simple setup process and a minimal learning curve
   * Manage machines very quickly and in parallel
   * Avoid custom-agents and additional open ports, be agentless by leveraging the existing SSH daemon
   * Describe infrastructure in a language that is both machine and human friendly
   * Focus on security and easy auditability/review/rewriting of content
   * Manage new remote machines instantly, without bootstrapping any software
   * Allow module development in any dynamic language, not just Python
   * Be usable as non-root
   * Be the easiest IT automation system to use, ever.

   * 최소한의 학습곡선과 최소화된 셋업
   * 병렬 상황에서 장치들을 빠르게 관리
   * 기 존재하는 SSH 데몬을 이용하여 에이전트가 없는 환경 설정. (커스텀 에이전트나 추가 포트의 사용을 제한함-회피함)
   * 장비와 사람 모두에게 친화적인(알기 쉬운) 언어로 구조를 표현함
   * 컨텐츠의 보안, 검사, 수정 기능에 집중함
   * 별도의 소프트웨어없이 새로운 원격장치를 관리할 수 있음
   * 파이썬 뿐 아니라 다양한 언어로 모듈 개발을 지원함
   * root 가 아닌 권한으로도 사용할 수 있음
   * 전에 없던 세상에서 가장 쉬운 IT 자동화 시스템


Get Involved
참여하기
============

   * Read [Community Information](https://docs.ansible.com/community.html) for all kinds of ways to contribute to and interact with the project, including mailing list information and how to submit bug reports and code to Ansible.
   * All code submissions are done through pull requests.  Take care to make sure no merge commits are in the submission, and use `git rebase` vs `git merge` for this reason.  If submitting a large code change (other than modules), it's probably a good idea to join ansible-devel and talk about what you would like to do or add first and to avoid duplicate efforts.  This not only helps everyone know what's going on, it also helps save time and effort if we decide some changes are needed.
   * Users list: [ansible-project](https://groups.google.com/group/ansible-project)
   * Development list: [ansible-devel](https://groups.google.com/group/ansible-devel)
   * Announcement list: [ansible-announce](https://groups.google.com/group/ansible-announce) - read only
   * irc.freenode.net: #ansible

   * [커뮤니티 정보](https://docs.ansible.com/community.html)파일을 읽기. 어떻게 프로젝트에 참여하는지, 메일링 리스트 정보, 버그 리포트 등 모든 정보가 담겨있음. 
   * 모든 코드 참여는 pull request 를 통해 이루어짐. 서브밋 할 때, 머지 커밋을 하지 않도록 주의바람.(동일한 이유로 `git rebase`나 `git merge` 도 마찬가지). 모듈이 아닌 영역에서 많은 코드 수정이 이루어지는 경우는 ansible-devel 에 참여해서 무엇을 하고 싶은지 밝히고 이미 하고 있는 작업이 아닌지 확인이 필요함. 이 작업은 뭐가 어떻게 돌아가고 싶은지 알고 싶은 사람들 뿐 아니라 우리가 무엇이 변경이 필요한지 결정하는데 필요한 시간들을 줄여줄 수 있음
   * 사용자 목록 : [ansible-project](https://groups.google.com/group/ansible-project)
   * 개발 목록 : [ansible-devel](https://groups.google.com/group/ansible-devel)
   * 공식 발표 : [ansible-renounce](https://groups.google.com/group/ansible-announce) - 읽기 전용
   *irc.freenode.net: #ansible


Branch Info
브랜치 정보
===========

   * Releases are named after Led Zeppelin songs. (Releases prior to 2.0 were named after Van Halen songs.)
   * The devel branch corresponds to the release actively under development.
   * For releases 1.8 - 2.2, modules are kept in different repos, you'll want to follow [core](https://github.com/ansible/ansible-modules-core) and [extras](https://github.com/ansible/ansible-modules-extras)
   * Various release-X.Y branches exist for previous releases.
   * We'd love to have your contributions, read [Community Information](https://docs.ansible.com/community.html) for notes on how to get started.

   * 릴리즈는 Led Zeppelin songs 를 따라서 이름붙여짐.(2.0 이전은 Van Helen songs 를 따라 이름 붙여졌음)
   * 개발(devel) 브랜치는 릴리즈가 활발하게 이루어지고 있음
   * 1.8 - 2.2 릴리즈는 모듈이 다른 리파지토리에 보관하고 있음. [core](https://github.com/ansible/ansible-modules-core) 와 [extras](https://github.com/ansible/ansible-modules-extras) 를 팔로우하는 걸 권장함
   * 이전 릴리즈에는 다양한 release-X.Y 브랜치들이 있음.
   * 당신들의 참여를 환영함. 참여하기 위해서 [커뮤니티 정보](https://docs.ansible.com/community.html)를 읽으시오.


Authors
작가들
=======

Ansible was created by [Michael DeHaan](https://github.com/mpdehaan) (michael.dehaan/gmail/com) and has contributions from over 1000 users (and growing).  Thanks everyone!

Ansible is sponsored by [Ansible, Inc](https://ansible.com)

Ansible은 [미쉘 드한](https://github.com/mpdehaan) (michael.dehaan/gmail/com)이 만들었고 1000 명이 넘는 사용자들이 참여하고 있음. 모두 감사!

Ansible은 [Ansible, Inc](https://ansible.com) 에서 스폰받고 있음


Licence
라이선스
=======
GNU
Click on the [Link](COPYING) to see the full text.

#### History
- 2017.05.04 : 초회 번역
