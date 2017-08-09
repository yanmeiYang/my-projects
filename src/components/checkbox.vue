<template>
	<div class="demo checkbox">
		<h3>
			<span class=“warning-signal”>#</span> 
			Checkbox
		</h3>
		<p>单个勾选框，逻辑值：</p>
		<figure class="code">
			<pre>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">input</span>
						<span class="attribute">type</span>=<span class="value">"checkbox"</span>
						<span class="attribute">id</span>=<span class="value">"checkbox"</span>
						<span class="attribute">v-model</span>=<span class="value">"checked"</span>&gt;
					</span>
				</span>	
				<br>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">label</span>
						<span class="attribute">for</span>=<span class="value">"checkbox"</span>&gt;
					</span>
					{{ "<code> checked </code> "}}
					<span class="tag">
						&lt;<span class="title">/label</span>&gt;
					</span>
				</span>
			</pre>
		</figure>
		<div class="example-2 example">
			<input type="checkbox" id="checkbox" v-model="checked">
			<label for="checkbox"> {{ checked }} </label>
		</div>
		<p>多个勾选框，绑定到同一个数组：</p>
		<figure class="code">
			<pre>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">input</span>
						<span class="attribute">type</span>=<span class="value">"checkbox"</span>
						<span class="attribute">id</span>=<span class="value">"jack"</span>
						<span class="attribute">value</span>=<span class="value">"Jack"</span>
						<span class="attribute">v-model</span>=<span class="value">"checkedNames"</span>&gt;
					</span>
				</span>
				<br>
				<span class="line">
					<sapn class="tag">
						&lt;<span class="title">label</span>
						<span class="attribute">for</span>=<span class="value">"Jack"</span>&gt;Jack&lt;<span class="title">/label</span>&gt;
					</sapn>
				</span>
				<br>
				<span class="line">
					<span class="tag">&lt;<span class="title">input</span>
					<span class="attribute">type</span>=<span class="value">"checkbox"</span>
					<span class="attribute">id</span>=<span class="value">"john"</span>
					<span class="attribute">value</span>=<span class="value">"John"</span>
					<span class="attribute">v-model</span>=<span class="value">checkedNames</span>&gt;</span>
				</span>
				<br>
				<span class="line">
					<sapn class="tag">
						&lt;<span class="title">label</span>
						<span class="attribute">for</span>=<span class="value">"John"</span>&gt;John&lt;<span class="title">/label</span>&gt;
					</sapn>
				</span>
				<br>
				<span class="line">
					<span class="tag">&lt;<span class="title">input</span>
					<span class="attribute">type</span>=<span class="value">"checkbox"</span>
					<span class="attribute">id</span>=<span class="value">"mike"</span>
					<span class="attribute">value</span>=<span class="value">"Mike"</span>
					<span class="attribute">v-model</span>=<span class="value">checkedNames</span>&gt;</span>
				</span>
				<br>
				<span class="line">
					<sapn class="tag">
						&lt;<span class="title">label</span>
						<span class="attribute">for</span>=<span class="value">"Mike"</span>&gt;Mike&lt;<span class="title">/label</span>&gt;
					</sapn>
				</span>
				<br>
				<span class="tag">
					&lt;br&gt;
				</span>
				<br>
				<span class="tag">
					&lt;<span class="title">span</span>&gt;
				</span>
				Checked names: {{ <code>checkedNames | json </code> }}
				<span class="tag">
					&lt;<span class="title">/span</span>&gt;
				</span>	
			</pre>
		</figure>
		<figure class="code">
			<pre>
				<span class="line"><span class="keyword">new</span> Vue({</span>
				<br>
				<span class="line"><span>&nbsp;&nbsp;el: '...',</span></span>
				<br>
				<span class="line"><span>&nbsp;&nbsp;data: {</span></span>
				<br>
				<span class="line"><span>&nbsp;&nbsp;&nbsp;&nbsp;checkedNames: []</span></span>
				<br>
				<span class="line"><span>&nbsp;&nbsp;}</span></span>
				<br>
				<span class="line"><span>})</span>
				
			</pre>
		</figure>
		<div class="example">
			<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
			<label for="jack">Jack</label>
			<input type="checkbox" id="john" value="John" v-model="checkedNames">
			<label for="john">John</label>
			<input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
			<label for="mike">Mike</label>
			<br>
			<span> Checked names: {{checkedNames}}</span>
		</div>
	</div>
</template>
<script>
export default {
  name: 'example-2',
  data () {
    return {
      checked: false,
      checkedNames: []
    }
  }
}
</script>
<style >
	figure {
		margin-right: 0px;
		margin-left: 0px;
	}
</style>