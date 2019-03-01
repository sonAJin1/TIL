---


---

<h1 id="mvvm에서의-view와-viewmodel">MVVM에서의 View와 ViewModel</h1>
<ul>
<li>
<p>View는 화면에 표시되는 레이아웃에 대해 관여합니다. 기본적으로 비지니스 모델에서 베제하지만 UI에 관련된 로직들을 수행합니다.</p>
</li>
<li>
<p>ViewModel은 View에 연결할 데이터와 명령으로 구현되어있으며 변경 알림을 통해서 뷰에게 상태 변화를 전달합니다.</p>
</li>
<li>
<p>전달받은 상태변화를 화면에 적용할지는 View에서 결정하게 합니다</p>
</li>
<li>
<p>명령은 UI를 통해서 동작하도록 합니다</p>
</li>
</ul>
<h1 id="view와-viewmodel의-관계">View와 ViewModel의 관계</h1>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-N466k0a957BazV00" height="100%" width="100%" style="max-width:650px;" viewBox="-50 -10 650 301"><g></g><g><line id="actor21" x1="75" y1="5" x2="75" y2="290" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="0" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="75" dy="0">View</tspan></text></g><g><line id="actor22" x1="275" y1="5" x2="275" y2="290" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="200" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="275" dy="0">View Model</tspan></text></g><g><line id="actor23" x1="475" y1="5" x2="475" y2="290" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="400" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="475" dy="0">Model</tspan></text></g><defs><marker id="arrowhead" refX="5" refY="2" markerWidth="6" markerHeight="4" orient="auto"><path d="M 0,0 V 4 L6,2 Z"></path></marker></defs><defs><marker id="crosshead" markerWidth="15" markerHeight="8" orient="auto" refX="16" refY="4"><path fill="black" stroke="#000000" stroke-width="1px" d="M 9,2 V 6 L16,4 Z" style="stroke-dasharray: 0, 0;"></path><path fill="none" stroke="#000000" stroke-width="1px" d="M 0,1 L 6,7 M 6,1 L 0,7" style="stroke-dasharray: 0, 0;"></path></marker></defs><g><text x="175" y="93" class="messageText" style="text-anchor: middle;">Data Binding and commands</text><line x1="75" y1="100" x2="275" y2="100" class="messageLine0" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="fill: none;"></line></g><g><text x="375" y="128" class="messageText" style="text-anchor: middle;">Model update</text><line x1="275" y1="135" x2="475" y2="135" class="messageLine0" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="fill: none;"></line></g><g><text x="175" y="163" class="messageText" style="text-anchor: middle;">Send notifiactions</text><line x1="275" y1="170" x2="75" y2="170" class="messageLine1" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><text x="375" y="198" class="messageText" style="text-anchor: middle;">Send notifiactions</text><line x1="475" y1="205" x2="275" y2="205" class="messageLine1" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><rect x="0" y="225" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="257.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="75" dy="0">View</tspan></text></g><g><rect x="200" y="225" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="257.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="275" dy="0">View Model</tspan></text></g><g><rect x="400" y="225" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="257.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="475" dy="0">Model</tspan></text></g></svg></div>
<ul>
<li>
<p>ViewModel은 Model은 알지만 View는 알지 못합니다.</p>
</li>
<li>
<p>View는 ViewModel은 알지만 Model을 알 수 없습니다</p>
</li>
<li>
<p>View는 ViewModel을 옵저빙 하고 있다가 상태가 변화하면 화면을 갱신해야 합니다.</p>
</li>
</ul>
<h1 id="databinding--view와-viewmodel의-독립">DataBinding : View와 ViewModel의 독립</h1>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-Xth3VCoxqP8iYbSz" height="100%" width="100%" style="max-width:650px;" viewBox="-50 -10 650 301"><g></g><g><line id="actor24" x1="75" y1="5" x2="75" y2="290" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="0" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="75" dy="0">ViewModel</tspan></text></g><g><line id="actor25" x1="275" y1="5" x2="275" y2="290" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="200" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="275" dy="0">DataBinding Class</tspan></text></g><g><line id="actor26" x1="475" y1="5" x2="475" y2="290" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="400" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="475" dy="0">XML(View)</tspan></text></g><defs><marker id="arrowhead" refX="5" refY="2" markerWidth="6" markerHeight="4" orient="auto"><path d="M 0,0 V 4 L6,2 Z"></path></marker></defs><defs><marker id="crosshead" markerWidth="15" markerHeight="8" orient="auto" refX="16" refY="4"><path fill="black" stroke="#000000" stroke-width="1px" d="M 9,2 V 6 L16,4 Z" style="stroke-dasharray: 0, 0;"></path><path fill="none" stroke="#000000" stroke-width="1px" d="M 0,1 L 6,7 M 6,1 L 0,7" style="stroke-dasharray: 0, 0;"></path></marker></defs><g><text x="175" y="93" class="messageText" style="text-anchor: middle;">데이터 변경 알림</text><line x1="75" y1="100" x2="275" y2="100" class="messageLine0" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="fill: none;"></line></g><g><text x="375" y="128" class="messageText" style="text-anchor: middle;">화면 변경 알림</text><line x1="475" y1="135" x2="275" y2="135" class="messageLine0" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="fill: none;"></line></g><g><text x="175" y="163" class="messageText" style="text-anchor: middle;">화면 정보 전달</text><line x1="275" y1="170" x2="75" y2="170" class="messageLine1" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><text x="375" y="198" class="messageText" style="text-anchor: middle;">데이터 전달</text><line x1="275" y1="205" x2="475" y2="205" class="messageLine1" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><rect x="0" y="225" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="257.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="75" dy="0">ViewModel</tspan></text></g><g><rect x="200" y="225" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="257.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="275" dy="0">DataBinding Class</tspan></text></g><g><rect x="400" y="225" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="257.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="475" dy="0">XML(View)</tspan></text></g></svg></div>
<ul>
<li>
<p>DataBinding은 View와 ViewModel 사이의 데이터와 명령을 연결해주어 각자의 존재를 명확하게 알지 못해도 다양한 인터랙션을 할 수 있게 도와주는 역할을 합니다.</p>
</li>
<li>
<p>DataBinding을 통해서 View와 ViewModel은 독립성을 더 높힐 수 있습니다</p>
</li>
</ul>

