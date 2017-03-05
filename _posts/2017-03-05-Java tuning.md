---
layout: post
title:  "자바 성능 튜닝"
date:   2017-03-05 20:20:10 +0800
categories: [tuning]
excerpt: 자바 성능 튜닝하기
tags:
  - Java
  - Tuning
  - back-end
---

<h1> 자바 성능 튜닝 </h1>

<br/>
<h4> List, Set, Map, Queue의 차이 </h4>

<figure class="highlight">
	<pre>
	<span class="s">List </span><span style="color:black">: 순서가 있는 집합을 처리하기 위한 인터페이스이다.
	       인덱스가 있어 위치를 지정하여 값을 찾을 수 있다. 중복 가능하다. </span><br/>
	<span class="s">Set </span><span style="color:black">: 집합을 처리하기 위한 인터페이스 이지만, List와는 달리 중복을 허용하지 않는다.
	      또한 인덱스도 없기 때문에 위치를 이용하여 값을 찾을 수 없다. </span><br/>
	<span class="s">Map </span><span style="color:black">: 키와 값을 쌍으로 구성된 객체의 집합을 처리하기 위한 인터페이스이다.
	      List보다는 Set과 비슷하고, 중복되는 키를 허용하지 않는다. </span><br/>
	<span class="s">Queue </span><span style="color:black">: 여러 개의 객체를 처리하기 전에 담아서 처리할 때 사용하는 인터페이스이며,
		FIFO(First in First Out)이다. </span></pre></figure>

<br/>
<h4> Reflection API를 이용하여 매개변수로 넘어온<br/>클래스의 종류 및 메소드 목록을 출력하는 메소드 작성 </h4>

<figure class="highlight">
	<pre>
	<span style="color:black">public void getClassInfo(Object classObj) {
		Class<? extends Object> inputClass = classObj.getClass();
		System.out.println("Class Name : " + inputClass.getName());<br/>
		Method[] methods = inputClass.getDeclaredMethods();
		System.out.println(inputClass.getSimpleName() + " Class's Methods");
		for ( Method method : methods) {
			System.out.println(method);
		}		
	}</span></pre></figure>

<br/>
<h4> XML 파서인 SAX와 DOM 파서의 특징 및 장단점 </h4>

<figure class="highlight">
	<pre>
	<span class="s">SAX(Simple API for Xml)</span>
	<span style="color:black">1. xml문서를 순차적으로 읽어 내려가며 노드가 열리고 닫히는 부분에서 이벤트가 발생
	2. xml문서 전체를 메모리에 올리지 않기 때문에 메모리 사용량이 적음.
	3. 단순히 읽기만 할 때 속도가 빠름.
	4. 발생한 이벤트를 핸들링하여 변수에 저장하고 활용하는 방식.
	   따라서 문서의 중간 중간 검색하고 노드를 수정하기 어려움
	5. dom방식에 비해 구현 방식이 복잡하고, 직관적이지 않음</span><br/>
	<span class="s">DOM(Document Object Model)</span>
	<span style="color:black">1. 처음 xml문서 전체를 메모리에 로드하여 값을 읽음
	2. xml문서 전체가 메모리에 올라가 있으르로 검색이 빠름.
	3. 데이터의 수정과 구조 변경이 쉬움
	4. sax방식에 비해 xml문서를 핸들링하는 것이 직관적임
</span></pre></figure>

<br/>
<h4> JMX란 </h4>

<figure class="highlight">
	<pre>
	<span class="s">Java Management Extensions</span>
	<span style="color:black">JMX는 자바 기반의 모든 애플리케이션을 모니터링하기 위해서 만든 기술이다.
	실제로 API는 웹서버에서 네트워크 디바이스, 웹폰에 이르기까지 자바로
	이용가능한 것은 어느것이든 로컬 혹은 원격으로 처리할 수 있게 한다. </span></pre></figure>

<br/>
<h4> JMX를 모니터링할 수 있는 도구들 </h4>

<figure class="highlight">
	<pre>
	<span style="color:black"><a href="https://visualvm.github.io/">Visual VM</a></span>
	<span style="color:black"><a href="http://docs.oracle.com/javase/6/docs/technotes/tools/share/jconsole.html">JConsole</a></span>
	<span style="color:black"><a href="https://sourceforge.net/projects/mc4j/">MC4J</a></span></pre></figure>

<br/>
<h4> Web Access Log의 패턴을 확인해보고, 각 패턴에 대해 서술하기 </h4>

<figure class="highlight">
	<pre>
	<span class="s">LogFormat "%h %l %u %t \"%r\" %>s %b" common</span><br/>
	<span class="s">%h </span><span style="color:black">: 서버에 요청한 클라이언트의  IP주소 </span>
	<span class="s">%l </span><span style="color:black">: Identd라는 사용자 인식 데몬이 클라이언트에서 동작하고 있을 때 정보가 나타남 </span>
	<span class="s">%u </span><span style="color:black">: HTTP인증을 통하여 확인된 문서를 요청한 사용자의 ID가 표시됨 </span>
	<span class="s">%t </span><span style="color:black">: 서버가 요청을 마친 시간을 표시함 </span>
	<span class="s">\"%r\" </span><span style="color:black">: 클라이언트에서 요청한 Request의 정보를 나타냄.
		 요청방식, 요청주소, 프로토콜의 종류와 버전순서로 표시됨 </span>
	<span class="s">%>s </span><span style="color:black">: 서버에서 클라이언트로 보낸 최종 상태 코드를 의미함 </span>
	<span class="s">%b </span><span style="color:black">: 클라이언트로 전송한 데이터의 크기가 표시됨 </span></pre></figure>

<br/>
<h4> 자바 GC의 종류 </h4>

<figure class="highlight">
	<pre>
	<span class="s">마이너GC </span><span style="color:black">: Young 영역에서 발생하는 GC </span>
	<span class="s">메이저GC </span><span style="color:black">: Old 영역이나 Perm 영역에서 발생하는 GC </span></pre></figure>

<br/>
<h4> GC상황을 모니터링할 수 있는 도구들 </h4>

<figure class="highlight">
	<pre>
	<span style="color:black"><a href="http://gceasy.io/">GC Analyzer</a></span>
	<span style="color:black"><a href="https://www.ibm.com/developerworks/community/groups/service/html/communityview?communityUuid=22d56091-3a7b-4497-b36e-634b51838e11">IBM GC 분석기</a></span>
	<span style="color:black"><a href="https://h20392.www2.hpe.com/portal/swdepot/displayProductInfo.do?productNumber=HPJTUNE">HPjtune</a></span></pre></figure>

<br/>
<h4> JMH를 사용하여 Java SE에 있는 List를 구현한 클래스들의<br/>추가/조회/삭제 기능의 성능 비교 </h4>

　<img style="margin-top: -25px;" src="/assets/images/list.png"/>

<br/>
<h4> JMH를 사용하여 Java SE에 있는 Map을 구현한 클래스들의<br/>추가/조회/삭제 기능의 성능 비교 </h4>

　<img style="margin-top: -25px;" src="/assets/images/map.png"/><br/>
<br/>


------

출처 : <a href="http://book.naver.com/bookdb/book_detail.nhn?bid=7333658">자바 성능 튜닝 이야기 - 이상민 지음</a>

출처 : <a href="https://www.google.co.kr/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiK9oOO9L7SAhXHvbwKHbgqC6UQFggmMAE&url=http%3A%2F%2Fwww.hansung.ac.kr%2Fweb%2Fwebp%2F513802%3Fp_p_id%3DEXT_BBS%26p_p_lifecycle%3D1%26p_p_state%3Dexclusive%26p_p_mode%3Dview%26p_p_col_id%3Dcolumn-1%26p_p_col_count%3D1%26_EXT_BBS_struts_action%3D%252Fext%252Fbbs%252Fget_file%26_EXT_BBS_extFileId%3D239730&usg=AFQjCNEyo_afiqVAtWRsPM85CMFfqHSKSQ&sig2=PMAWuDRAILXU6FyLm81AUA">JMX 기술의 이해</a>

출처 : <a href="http://stg.etribe.co.kr/2014/08/09/xml-%ED%8C%8C%EC%8B%B1%EC%8B%9C-dom%EA%B3%BC-sax%EC%9D%98-%EC%B0%A8%EC%9D%B4/">Etribe Programmer's Blog</a>