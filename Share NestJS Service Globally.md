---


---

<p>In NestJS, you can make a service available across all modules by declaring it in a global module. Here are the steps to do it:</p>
<ol>
<li>
<p><strong>Create a Service</strong>: If you haven’t already, create the service that you want to share using the NestJS CLI. For instance, to create a service called <code>AppService</code>, you would run the following command:</p>
<pre><code>nest g service app
</code></pre>
</li>
<li>
<p><strong>Create a Global Module</strong>: Next, create a module that you will declare as a global module. This could be the same module that the service is a part of, or it could be a separate module. For this example, let’s assume you’re creating a new module called <code>GlobalModule</code>:</p>
<pre><code>nest g module global
</code></pre>
</li>
<li>
<p><strong>Declare the Module as Global</strong>: In the <code>global.module.ts</code> file, you need to add the <code>@Global()</code> decorator from <code>@nestjs/common</code> to declare the module as a global module:</p>
<pre class=" language-typescript"><code class="prism  language-typescript"><span class="token keyword">import</span> <span class="token punctuation">{</span> Global<span class="token punctuation">,</span> Module <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">'@nestjs/common'</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token punctuation">{</span> AppService <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">'./app.service'</span><span class="token punctuation">;</span>

@<span class="token function">Global</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
@<span class="token function">Module</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
  providers<span class="token punctuation">:</span> <span class="token punctuation">[</span>AppService<span class="token punctuation">]</span><span class="token punctuation">,</span>
  exports<span class="token punctuation">:</span> <span class="token punctuation">[</span>AppService<span class="token punctuation">]</span><span class="token punctuation">,</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token keyword">export</span> <span class="token keyword">class</span> <span class="token class-name">GlobalModule</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
</code></pre>
<p>In this code, the <code>AppService</code> is provided and exported by the <code>GlobalModule</code>, which is marked as global with the <code>@Global()</code> decorator.</p>
</li>
<li>
<p><strong>Use the Service</strong>: Now, the <code>AppService</code> can be imported and used in any module in your NestJS application without needing to import the <code>GlobalModule</code>:</p>
<pre class=" language-typescript"><code class="prism  language-typescript"><span class="token keyword">import</span> <span class="token punctuation">{</span> Module <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">'@nestjs/common'</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token punctuation">{</span> AppService <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">'./app.service'</span><span class="token punctuation">;</span>

@<span class="token function">Module</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
  providers<span class="token punctuation">:</span> <span class="token punctuation">[</span>AppService<span class="token punctuation">]</span><span class="token punctuation">,</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token keyword">export</span> <span class="token keyword">class</span> <span class="token class-name">SomeOtherModule</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
</code></pre>
<p>In this code, the <code>AppService</code> is imported and provided in <code>SomeOtherModule</code>, even though <code>GlobalModule</code> is not imported.</p>
</li>
</ol>
<p>Remember that while global modules can be very convenient, they should be used sparingly, as they can make it harder to understand which parts of your application depend on which other parts. It’s usually best to explicitly import the modules that you depend on.</p>

