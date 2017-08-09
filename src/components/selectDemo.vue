<template>
	<div class="demo select-example">
		<h3>
			<span class=“warning-signal”>#</span> 
			Select
		</h3>
		<p>单选： </p>
		<figure class="code">
			<pre>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">select</span>&nbsp;<span class="attribute">v-model</span>=<span class="value">"selected"</span>&gt;
					</span>
					<br>
					<span class="tag">
						&nbsp;&nbsp;&lt;<span class="title">option</span>&nbsp;<span class="attribute">selected</span>&gt;
					</span>
					A
					<span class="tag">&lt;<span class="title">/option</span>&gt;</span>
					</span>
					<br>
					<span class="tag">
						&nbsp;&nbsp;&lt;<span class="title">option</span>&gt;
					</span>
					B
					<span class="tag">&lt;<span class="title">/option</span>&gt;</span>
					</span>
					<br>
					<span class="tag">
						&nbsp;&nbsp;&lt;<span class="title">option</span>&gt;
					</span>	
					C
					<sapn class="tag">&lt;<span class="title">/option</span>&gt;</sapn>
					</span>
					<br>
					<span class="tag">
						&lt;<span class="title">/select</span>&gt;
					</span>
				</span>
				<br>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">span</span>&gt;
					</span>
					Selected: {<span>{selected }}</span>
					<span class="tag">
						&lt;<span class="title">/span</span>&gt;
					</span>
				</span>
			</pre>	
		</figure>
		<div class="example">
			<select>
				<option value="A" selected>A</option>
				<option value="B">B</option>
				<option value="C">C</option>
			</select>
			<span>Selected: {{selected}} </span>
		</div>
		<p>多选（绑定到一个数组）： </p>
		<figure class="code">
			<pre>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">select</span>&nbsp;<span class="attribute">v-model</span>=<span class="value">"selected"</span>&nbsp;<span class="value">multiple</span>&nbsp;&gt;
					</span>
					<br>
					<span class="tag">
						&nbsp;&nbsp;&lt;<span class="title">option</span> &nbsp;<span class="value">selected</span>&gt;
					</span>
					A
					<span class="tag">
						&lt;<span class="title">/option</span>&gt;
					</span>
					<br>
					<span class="tag">
						&nbsp;&nbsp;&lt;<span class="title">option</span>&gt;
					</span>
					B
					<span class="tag">
						&lt;<span class="title">/option</span>&gt;
					</span>
					<br>
					<span class="tag">
						&nbsp;&nbsp;&lt;<span class="title">option</span>&gt;
					</span>
					C
					<span class="tag">
						&lt;<span class="title">/option</span>&gt;
					</span>
					<br>
					<span class="tag">
						&lt;<span class="title">select</span>&gt;
					</span>
					<span class="tag">
						&lt;<span class="title">br</span>&gt;
					</span>
					<span class="tag">
						&lt;<span class="title">span</span>
					</span>
					Selected: {{ selected | json }}
					<span class="tag">
						&lt;<span class="title">/span</span>&gt;
					</span>
				</span>
				<span class="line"></span>				
				<span class="line"></span>
			</pre>
		</figure>
		<div class="example">
			<select multiple v-model="selectedMore">
				<option value="" selected>A</option>
				<option value="">B</option>
				<option value="">C</option>
			</select>
			<br>
			<span>Selected: {{ selectedMore | json }}</span> 
		</div>
</template>
<script>
export default {
  name: 'select-example',
  data () {
    return {
      selected: 'A',
      selectedMore: 'A'
    }
  }
}
</script>