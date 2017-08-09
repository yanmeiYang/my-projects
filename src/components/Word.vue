<template>
	<div class="word">
		<h1>表单控件绑定</h1>
		<h2>基础用法</h2>
		<hr>
		<p>可以用<code>v-model</code>指令在表单控件元素上创建双向数据绑定。根据控件类型它自动选取正确的方法更新元素。尽管有点神奇，<code>v-model</code>不过是语法糖，在用户输入事件中更新数据，以及特别处理一些极端例子。
		</p>
		<h3>
			<span class=“warning-signal”>#</span> 
			Text
		</h3>
		<figure class="highlight html">
			<table>
				<tbody>
					<tr>	
						<td class="code">
							<pre>
								<span class="line">
									<span class="tag">&lt;<span class="title">span</span>&gt;</span>
									Message is: {<code>{ message </code>}}
									<span class="tag">&lt;/<span class="title">span</span>&gt;</span>
								</span>
								<br>
								<span class="line">
									<span class="tag">&lt;<span class="title">br</span>&gt;</span>
								</span>
								<br>
								<span class="line">
									<span class="tag">
										&lt;<span class="title">input</span> 
										<span class="attribute">type</span>=<span class="value">"text"</span> 
										<span class="attribute">v-model</span>=<span class="value">"message"</span> 
										<span class="attribute">placeholder</span>=<span class="value">"edit me"</span>&gt;
									</span>
								</span>
								<br>
							</pre>
						</td>
					</tr>
				</tbody>
			</table>
		</figure>
		<div class="example example-1">
			<span> Message is {{ message }}</span>
			<br>
			<input type="text" v-model="message" placeholder="edit me">
		</div>
		<checkbox></checkbox>
		<radio></radio>
		<selectDemo></selectDemo>
	</div>
</template>
<script>
import checkbox from './checkbox'
import radio from './radio'
import selectDemo from './selectDemo'

export default {
  name: 'example-1',
  components: {
    'checkbox': checkbox,
    'radio': radio,
    'selectDemo': selectDemo
  },
  data () {
    return {
      message: ''
    }
  }
}
</script>
<style>
	.word{
		text-align: left;
		width:50%;
		margin:0 auto;
	}
	.warning-signal{
		color:#42b983;
	}
	.code pre {
		padding: 1.2em 1.4em;
		line-height: 1.5em;
		margin: 0 auto;
		white-space: normal;
	}
	.code, pre {
		font-family: 'Roboto Mono', Monaco, courier, monospace;
		font-size: 0.8em;
		background-color: #f8f8f8;
		-webkit-font-smoothing: initial;
	}
	pre .tag, pre .tag .title, pre .change, pre .winutils, pre .flow, pre .lisp .title, pre .clojure .built_in, pre .nginx .title, pre .tex .special {
		color: #2973b7;
	}
	pre .keyword, pre .attribute {
	    color: #e96900;
	  }
	pre .tag .value {
		 color: #42b983;
	}  
	.example {
		border: 1px solid #eee; border-radius: 2px;padding: 10px
	}

</style>