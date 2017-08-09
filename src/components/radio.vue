<template>
	<div class="demo radio-example">
		<h3>
			<span class=“warning-signal”>#</span> 
			Radio
		</h3>
		<figure class="code">
			<pre>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">input</span>
						<span class="attribute">type</span>=<span class="value">"radio"</span>
						<span class="attribute">id</span>=<span class="value">"one"</span>
						<span class="attribute">value</span>=<span class="value">"One"</span>
						<span class="attribute">v-model</span>=<span class="value">"picked"</span>&gt;
					</span>
				</span>
				<br>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">label</span>
						<span class="attribute">for</span>=<span class="value">"one"</span>&gt;One&lt;<span class="title">/label</span>&gt;
					</span>
				</span>
				<br>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">br</span>&gt;
					</span>
				</span>
				<br>
				<span class="line">
					<sapn class="tag">
						&lt;<span class="title">input</span>
						<span class="attribute">type</span>=<span class ="value">"radio"</span>
						<span class="attribute">id</span>=<span class="value">"two"</span>
						<span class="attribute">value</span>=<span class="value">"Two"</span>
						<span class="attribute">v-model</span>=<span class="value">"picked"</span>
					</sapn>
				</span>
				<br>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">label</span>
						<span class="attribute">for</span>=<span class="value">"two"</span>&gt;Two&lt;<span class="title">/label</span>&gt;
					</span>
				</span>
				<br>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">br</span>&gt;
					</span>
				</span>
				<br>
				<span class="line">
					<span class="tag">
						&lt;<span class="title">span</span>&gt;
					</span>
				</span>	
				<span> Picked: {</span>
				<span>{ picked </span> 
				<span> }} </span>
				<span class="line">
					<span class="tag">
						 &lt;<span class="title">/span</span>&gt;
					</span>
				</span>	
			</pre>
		</figure>
		<div class="example">
			<input type="radio" id="one" value="One" v-model="picked">
			<label for="one">One</label>
			<br>
			<input type="radio" id="two" value="Two" v-model="picked">
			<label for="two">Two</label>
			<br>
			<span> Picked: {{ picked }}</span>
		</div>
	</div>
</template>
<script>
export default {
  name: 'radio-example',
  data () {
    return {
      picked: ''
    }
  }
}
</script>