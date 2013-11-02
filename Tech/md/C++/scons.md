#Scons学习笔记
##安装
<pre>
Mac Os brew install scons
</pre>

##build
* 创建一个<code>SConstruct</code>文件，写入<code>Program(’hello.c’)</code>
* 指定输出文件名字</br>
<code>Program(’new_hello’, ’hello.c’)</code>,target Name 后跟source file name
* 多个source文件</br>
	1. <code>Program([’prog.c’, ’file1.c’, ’file2.c’])</code>默认最终的输出文件为prog</br>
	<pre>
	% scons -Q
	</pre>
	* 指定target Name，<code>Program(’mytargetname’, [’prog.c’, ’file1.c’, ’file2.c’])</code>
	<pre>
	% scons -Q
	</pre>
	* 使用Glob函数获取文件列表<code> Program(’program’, Glob(’*.c’))</code>，支持正则表达式</br>
	或：
	<pre>
	Program(’program’, Split(’main.c file1.c file2.c’))
	Program(’program’, src_files)
	</pre>
	* 使用关键字指定
	<pre>
	src_files = Split(’main.c file1.c file2.c’)
	</pre>
* 多个source文件</br>


## Building and Linking with Libraries##
#build libraries#
* 使用Library编译静态库</br><code>Library(’foo’, [’f1.c’, ’f2.c’, ’f3.c’])</code>
<pre>
% scons -Q
</pre>
* 创建库的时候，源文件可以是<code>.o</code>或者<code>.cpp</code>均可  
* StaticLibrary与Library功能上相同
* 使用<code>SharedLibrary</code>创建DLL库
<code>SharedLibrary(’foo’, [’f1.c’, ’f2.c’, ’f3.c’])</code>
<pre>
% scons -Q
</pre>

#link libraries#
* 使用<code>$LIBS</code>指定库文件，使用<code>$LIBPATH</code>指定库所在的路径
<pre>
Library(’foo’, [’f1.c’, ’f2.c’, ’f3.c’])
</pre>
* 不必指定库文件前缀或后缀
* <code>$LIBPATH</code>可以指定多个文件路径，或者用系统指定的路径分隔符拼成的字符串。
<pre>
Program(’prog.c’, LIBS = ’m’,
LIBPATH = ’/usr/lib:/usr/local/lib’
LIBPATH = ’C:\\lib;D:\\lib’                                 
</pre>




##run##
* 执行<code>scons</code>命令
* <code>scons -Q</code> 删掉中间打印的消息
* 

##clean up##
<pre>
<code>scons -c</code>
</pre>



##其他##
* SConstruct 与 makefile的区别是，Sconstruct实际是一个python脚本
* SCons Functions Are Order-Independent</br>
<pre>
	   print "Calling Program(’hello.c’)"
</pre>