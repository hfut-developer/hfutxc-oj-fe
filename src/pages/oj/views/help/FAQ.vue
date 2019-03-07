<template>
  <panel>
    <div slot="title">{{$t('m.Frequently_Asked_Questions')}}</div>
    <div class="content markdown-body">
      <ul>
        <li>这个在线裁判系统使用什么样的编译器和编译选项?
          <p>
              系统运行于<a href="http://www.debian.org/">Debian</a>/<a href="http://www.ubuntu.com">Ubuntu</a> Linux. 使用<a href="http://gcc.gnu.org/">GNU GCC/G++</a> 作为C/C++编译器, <a href="http://www.freepascal.org">Free Pascal</a> 作为pascal 编译器 ，用 <a href="http://www.oracle.com/technetwork/java/index.html">sun-java-jdk1.6</a> 编译 Java. 对应的编译选项如下:<br>
          </p>
          <table border="1">
          <tbody><tr>
            <td>C:</td>
            <td><font color="blue">gcc Main.c -o Main  -fno-asm -O2 -Wall -lm --static -std=c99 -DONLINE_JUDGE</font></td>
          </tr>
            <tr>
              <td>C++:</td>
              <td><font color="blue">g++ Main.cc -o Main  -fno-asm -O2 -Wall -lm --static -DONLINE_JUDGE</font></td>
            </tr>
            <tr>
              <td>Pascal:</td>
              <td><font color="blue">fpc Main.pas -oMain -O1 -Co -Cr -Ct -Ci </font></td>
            </tr>
            <tr>
              <td>Java:</td>
              <td><font color="blue">javac -J-Xms32m -J-Xmx256m Main.java</font>
              <br>
              <font size="-1" color="red">*Java has 2 more seconds and 512M more memory when running and judging.</font>
              </td>
            </tr>
          </tbody></table>
          <p>  编译器版本为（系统可能升级编译器版本，这里只供参考）:<br>
            <font color="blue">gcc (Ubuntu/Linaro 4.4.4-14ubuntu5) 4.4.5</font><br>
            <font color="blue">glibc 2.3.6</font><br>
          <font color="blue">Free Pascal Compiler version 2.4.0-2 [2010/03/06] for i386<br>
          java version "1.6.0_22"<br>
          </font></p>
        </li>
        <li>程序怎样取得输入、进行输出?
          <p>你的程序应该从标准输入 stdin('Standard Input')获取输出 并将结果输出到标准输出 stdout('Standard Output').例如,在C语言可以使用 'scanf' ，在C++可以使用'cin' 进行输入；在C使用 'printf' ，在C++使用'cout'进行输出.</p>
          <p>用户程序不允许直接读写文件, 如果这样做可能会判为运行时错误 "<font color="green">Runtime Error</font>"。<br>
            <br>
          下面是 1000题的参考答案</p>
          <p> C++:<br>
          </p>
          <pre><font color="blue">
          #include &lt;iostream&gt;
          using namespace std;
          int main(){
              int a,b;
              while(cin &gt;&gt; a &gt;&gt; b)
                  cout &lt;&lt; a+b &lt;&lt; endl;
            return 0;
          }
          </font></pre>
          C:<br>
          <pre><font color="blue">
          #include &lt;stdio.h&gt;
          int main(){
              int a,b;
              while(scanf("%d %d",&amp;a, &amp;b) != EOF)
                  printf("%d\n",a+b);
            return 0;
          }
          </font></pre>
          PASCAL:<br>
          <pre><font color="blue">
          program p1001(Input,Output); 
          var 
            a,b:Integer; 
          begin 
            while not eof(Input) do 
              begin 
                Readln(a,b); 
                Writeln(a+b); 
              end; 
          end.
          </font></pre>
          <br><br>

          Java:<br>
          <pre><font color="blue">
          import java.util.*;
          public class Main{
            public static void main(String args[]){
              Scanner cin = new Scanner(System.in);
              int a, b;
              while (cin.hasNext()){
                a = cin.nextInt(); b = cin.nextInt();
                System.out.println(a + b);
              }
            }
          }</font></pre>
        </li>
        <li>为什么我的程序在自己的电脑上正常编译，而系统告诉我编译错误!
          <p>
            GCC的编译标准与VC6有些不同，更加符合c/c++标准:<br>
            <ul>
              <li><font color="blue">main</font> 函数必须返回<font color="blue">int</font>, <font color="blue">void main</font> 的函数声明会报编译错误。<br> 
              </li><li><font color="green">i</font> 在循环外失去定义 "<font color="blue">for</font>(<font color="blue">int</font> <font color="green">i</font>=0...){...}"<br>
              </li><li><font color="green">itoa</font> 不是ansi标准函数.<br>
              </li><li><font color="green">__int64</font> 不是ANSI标准定义，只能在VC使用, 但是可以使用<font color="blue">long long</font>声明64位整数。<br>如果用了__int64,试试提交前加一句#define __int64 long long
            </li></ul>
          </p>
        </li>
        <li>系统返回信息都是什么意思?
          <p>
            详见下述:<br>
          <p><font color="blue">Pending</font> : 系统忙，你的答案在排队等待. </p>
          <p><font color="blue">Pending Rejudge</font>: 因为数据更新或其他原因，系统将重新判你的答案.</p>
          <p><font color="blue">Compiling</font> : 正在编译.<br>
          </p>
          <p><font color="blue">Running &amp; Judging</font>: 正在运行和判断.<br>
          </p>
          <p><font color="blue">Accepted</font> : 程序通过!<br>
            <br>
            <font color="blue">Presentation Error</font> : 答案基本正确，但是格式不对。<br>
            <br>
            <font color="blue">Wrong Answer</font> : 答案不对，仅仅通过样例数据的测试并不一定是正确答案，一定还有你没想到的地方.<br>
            <br>
            <font color="blue">Time Limit Exceeded</font> : 运行超出时间限制，检查下是否有死循环，或者应该有更快的计算方法。<br>
            <br>
            <font color="blue">Memory Limit Exceeded</font> : 超出内存限制，数据可能需要压缩，检查内存是否有泄露。<br>
            <br>
            <font color="blue">Output Limit Exceeded</font>: 输出超过限制，你的输出比正确答案长了两倍.<br>
            <br>
            <font color="blue">Runtime Error</font> : 运行时错误，非法的内存访问，数组越界，指针漂移，调用禁用的系统函数。请点击后获得详细输出。<br>
          </p>
          <p>  <font color="blue">Compile Error</font> : 编译错误，请点击后获得编译器的详细输出。<br>
            <br>
          </p>
        </li>
        <li>如何参加在线比赛?
          <p>
            <a href="registerpage.php">注册</a> 一个帐号，然后就可以练习，点击比赛列表Contests可以看到正在进行的比赛并参加。<br><br>
          </p>
        </li>
        <li>Where is the input and the output?
          <p>Your program shall read input from <code>stdin</code>('Standard Input') and write output to <code>stdout</code>('Standard Output').
            For example,you can use <code>scanf</code> in C or <code>cin</code> in C++ to read from stdin,and use <code>printf</code> in C or <code>cout</code> in C++ to write to stdout.
            User programs are not allowed to read or write files, or you will get a <code>Runtime Error</code>.
          </p>
        </li>
        <li>What's the meaning of the submission execution time?
        <p>The onlinejudge might test your code multiple times with different input files.
          If your code gives the correct answer within the time limit for each input file, the execution time displayed is the max of the time spent for each test case.
          Otherwise, the execution time will have no sense.
        </p>
        </li>
        <li>How can I use C++ Int64?
          <p>You should declare as <code>long long</code> and use with <code>cin/cout</code> or <code>%lld</code>, using<code> __int64</code> will result in <code>Compile Error</code>.</p>
        </li>
        <li>Java specifications?
          <p>All programs must begin in a static main method in a <code>Main</code> class. Do not use public classes: even <code>Main</code> must be non public to avoid compile error.Use buffered I/O to avoid time limit exceeded due to excesive flushing.</p>
        </li>
        <li>About presentation error?
          <p>There is no presentation error in this oj.The judger will trim the blacks and wraps in your ouput's <b>last</b> line.
            if it's still different with the correct output, the result will be <code>Wrong Answer</code>.</p>
        </li>
        <li>How to report bugs about this oj?
          <p>The onlinejudge is open source, you can open an issue in <a href="https://github.com/QingdaoU/OnlineJudge">Github</a>.
            The details(like env, version..) about a bug is required, which will help us a lot to solve the bug.
            Certainly, we are very pleased to merge your pull requests.
          </p>
        </li>
        <li>
          <p>
          </p>
        </li>
      </ul>
    </div>
  </panel>
</template>

<script>
</script>

<style lang="less" scoped>
  .content {
    font-size: 16px;
    margin: 0 50px 40px 50px;
    > ul {
      list-style: disc;
      li {
        font-size: 16px;
        margin-top: 20px;
        &:first-child {
          margin-top: 0;
        }
        p {
          font-size: 14px;
          margin-top: 5px;
        }
      }
    }
  }
</style>
