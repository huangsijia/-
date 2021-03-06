## 正则表达式的定义
      正则表达式的对象可以用两种方式创建：
      1、直接量（推荐）
      正则表达式的直接量是包含在一对斜杠（/）之间的字符，如：
      var pattern=/s$/;
      以上代码创建了一个新的正则对象，并将它赋值给变量pattern。

      2、构造函数（当正则表达式是动态的时候可以使用这种）
       var pattern=new RegExp("s$");
      以构造函数的方式创建一个新的正则表达式对象。

## 转义符
      正则表达式中的所有字母和数字都是按照字面含义进行匹配的，但是也支持非字母的字符匹配，这些字符需要通过反斜线（\）作为前缀进行转义。
      在正则中转义符也是通过反斜杠（\）来表示。
      如果我们需要匹配一个反斜杠（\），则我们需要输入两个反斜杠（\\）。

      当我们需要在正则表达式中使用特殊字符的直接量时，需要在特殊字符前面添加转义符（\），另一种方式就是将特殊字符放到中括号[ ]中也能表示特殊字符的直接量。
      字符
      匹配
      字母和数字字符
      自身
      \o
      NUL字符（\u0000）
      \t
      制表符（\u0009）
      \n	
      换行符(\u000A)
      \v
      垂直制表符（\u000b）
      \f	换页符（\u000C）
      \r	回车符（\u000D）

      需要特别注意的某些特定的字母和数字在有反斜线做前缀有了特殊的意义。
      字符	
      匹配
      [...]
      方括号中的任意字符
      [^....]	
      不在方括号中的任意字符
      .
      除换行符和其他Unicode行终止符之外的任意字符。
      \w
      任何ASCII字符组成的单词，等价于[a-zA-Z0-9]
      \W	任何非ASCII字符组成的单词，等价于[^a-zA-Z0-9]
      \s
      匹配任何空白字符，包括空格、制表符、换页符等等。等价于 [ \f\n\r\t\v]。
      \S
      匹配任何非空白字符。等价于 [^ \f\n\r\t\v]。

## 特殊字符
      特殊字符
      描述
      ^
      匹配输入字符串的开始位置，除非在方括号表达式中使用，此时它表示不接受该字符集合。要匹配 ^ 字符本身，请使用 \^。
      $	
      匹配输入字符串的结尾位置。如果设置了 RegExp 对象的 Multiline 属性，则 $ 也匹配 '\n' 或 '\r'。要匹配 $ 字符本身，请使用 \$。
      ( )
      标记一个子表达式的开始和结束位置。子表达式可以获取供以后使用。要匹配这些字符，请使用 \( 和 \)。
      *
      匹配前面的子表达式零次或多次。要匹配 * 字符，请使用 \*。
      +
      匹配前面的子表达式一次或多次。要匹配 + 字符，请使用 \+。
      .
      匹配除换行符 \n之外的任何单字符。要匹配 .，请使用 \。
      [
      标记一个中括号表达式的开始。要匹配 [，请使用 \[。
      ?
      匹配前面的子表达式零次或一次，或指明一个非贪婪限定符。要匹配 ? 字符，请使用 \?。
      \
      将下一个字符标记为或特殊字符、或原义字符、或向后引用、或八进制转义符。例如， 'n' 匹配字符 'n'。'\n' 匹配换行符。序列 '\\' 匹配 "\"，而 '\(' 则匹配 "("。
      {
      标记限定符表达式的开始。要匹配 {，请使用 \{。
      |
      指明两项之间的一个选择。要匹配 |，请使用 \|。

## 限定符
      限定符用来指定正则表达式的一个给定组件必须要出现多少次才能满足匹配，共有6种：
      字符	
      描述
      *
      匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。
      +
      匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。
      ?
      匹配前面的子表达式零次或一次。例如，"do(es)?" 可以匹配 "do" 或 "does" 中的"do" 。? 等价于 {0,1}。
      {n}
      n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。
      {n,}
      n 是一个非负整数。至少匹配n 次。例如，'o{2,}' 不能匹配 "Bob" 中的 'o'，但能匹配 "foooood" 中的所有 o。'o{1,}' 等价于 'o+'。'o{0,}' 则等价于 'o*'。
      {n,m}
      m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。例如，"o{1,3}" 将匹配 "fooooood" 中的前三个 o。'o{0,1}' 等价于 'o?'。请注意在逗号和两个数之间不能有空格。
      *、+和?限定符都是贪婪的，因为它们会尽可能多的匹配文字，只有在它们的后面加上一个?就可以实现非贪婪或最小匹配。
      通过在 *、+ 或 ? 限定符之后放置 ?，该表达式从"贪心"表达式转换为"非贪心"表达式或者最小匹配。

      注意：在使用*和?限定符时要注意，因为其可以表示0次匹配，因此他们允许什么都不匹配。比如正则表达式/a*/它与bbbb是匹配的。因为这个字符串 有0个a。


## 贪婪匹配和非贪婪匹配
      正则表达式的匹配默认是贪婪匹配的，在使用限定符*，+，？，{n,},{n,m}进行匹配时，正则表达式会尽可能多的去匹配。
      比如：正则表达式/a*/，匹配字符串“aaaaaaaaaa”,它会匹配整个字符串,这就是正则表达式的默认的贪婪匹配。
      当然我们也可以设置其非贪婪匹配，也就是说让它尽可能少的去匹配 在限定符后跟随一个问号即可：“*？”，“+？”，“？？”，“{n,}?”,"{n,m}?"
      这样当正则匹配的时候它会尽可能少的去匹配。

      说白点：就是当我们使用的限定符有匹配最少次和匹配最多次时，正则表达式默认匹配最多次（贪婪匹配），当给限定符后跟一个问号?时，其就匹配最少次数（非贪婪匹配）。
      比如：/a*/，因为*限定符是匹配0次或者无限次，故默认它会匹配无限次，当限定符后跟?时（/a*?/），它就匹配0次。
      <script>
      var reg = /a+/; //贪婪匹配
      var regs=/a+?/; //非贪婪匹配
      console.log("aaaaaaaaaabbbccc".match(reg).toString());   //aaaaaaaaaa
      console.log("aaaaaaaaaabbbccc".match(regs).toString());  //a
      </script>




## 元字符
      字符	描述
      \	将下一个字符标记为一个特殊字符、或一个原义字符、或一个 向后引用、或一个八进制转义符。例如，'n' 匹配字符 "n"。'\n' 匹配一个换行符。序列 '\\' 匹配 "\" 而 "\(" 则匹配 "("。
      ^	匹配输入字符串的开始位置。如果设置了 RegExp 对象的 Multiline 属性，^ 也匹配 '\n' 或 '\r' 之后的位置。
      $	匹配输入字符串的结束位置。如果设置了RegExp 对象的 Multiline 属性，$ 也匹配 '\n' 或 '\r' 之前的位置。
      *	匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。
      +	匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。
      ?	匹配前面的子表达式零次或一次。例如，"do(es)?" 可以匹配 "do" 或 "does" 中的"do" 。? 等价于 {0,1}。
      {n}	n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。
      {n,}	n 是一个非负整数。至少匹配n 次。例如，'o{2,}' 不能匹配 "Bob" 中的 'o'，但能匹配 "foooood" 中的所有 o。'o{1,}' 等价于 'o+'。'o{0,}' 则等价于 'o*'。
      {n,m}	m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。例如，"o{1,3}" 将匹配 "fooooood" 中的前三个 o。'o{0,1}' 等价于 'o?'。请注意在逗号和两个数之间不能有空格。
      ?	当该字符紧跟在任何一个其他限制符 (*, +, ?, {n}, {n,}, {n,m}) 后面时，匹配模式是非贪婪的。非贪婪模式尽可能少的匹配所搜索的字符串，而默认的贪婪模式则尽可能多的匹配所搜索的字符串。例如，对于字符串 "oooo"，'o+?' 将匹配单个 "o"，而 'o+' 将匹配所有 'o'。
      .	匹配除 "\n" 之外的任何单个字符。要匹配包括 '\n' 在内的任何字符，请使用象 '[.\n]' 的模式。
      (pattern)	匹配 pattern 并获取这一匹配。所获取的匹配可以从产生的 Matches 集合得到，在VBScript 中使用 SubMatches 集合，在JScript 中则使用 $0…$9 属性。要匹配圆括号字符，请使用 '\(' 或 '\)'。
      (?:pattern)	匹配 pattern 但不获取匹配结果，也就是说这是一个非获取匹配，不进行存储供以后使用。这在使用 "或" 字符 (|) 来组合一个模式的各个部分是很有用。例如， 'industr(?:y|ies) 就是一个比 'industry|industries' 更简略的表达式。
      (?=pattern)	正向预查，在任何匹配 pattern 的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。例如，'Windows (?=95|98|NT|2000)' 能匹配 "Windows 2000" 中的 "Windows" ，但不能匹配 "Windows 3.1" 中的 "Windows"。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始。
      (?!pattern)	负向预查，在任何不匹配 pattern 的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。例如'Windows (?!95|98|NT|2000)' 能匹配 "Windows 3.1" 中的 "Windows"，但不能匹配 "Windows 2000" 中的 "Windows"。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始。
      x|y	匹配 x 或 y。例如，'z|food' 能匹配 "z" 或 "food"。'(z|f)ood' 则匹配 "zood" 或 "food"。
      [xyz]	字符集合。匹配所包含的任意一个字符。例如， '[abc]' 可以匹配 "plain" 中的 'a'。
      [^xyz]	负值字符集合。匹配未包含的任意字符。例如， '[^abc]' 可以匹配 "plain" 中的'p'、'l'、'i'、'n'。
      [a-z]	字符范围。匹配指定范围内的任意字符。例如，'[a-z]' 可以匹配 'a' 到 'z' 范围内的任意小写字母字符。
      [^a-z]	负值字符范围。匹配任何不在指定范围内的任意字符。例如，'[^a-z]' 可以匹配任何不在 'a' 到 'z' 范围内的任意字符。
      \b	匹配一个单词边界，也就是指单词和空格间的位置。例如， 'er\b' 可以匹配"never" 中的 'er'，但不能匹配 "verb" 中的 'er'。
      \B	匹配非单词边界。'er\B' 能匹配 "verb" 中的 'er'，但不能匹配 "never" 中的 'er'。
      \cx	匹配由 x 指明的控制字符。例如， \cM 匹配一个 Control-M 或回车符。x 的值必须为 A-Z 或 a-z 之一。否则，将 c 视为一个原义的 'c' 字符。
      \d	匹配一个数字字符。等价于 [0-9]。
      \D	匹配一个非数字字符。等价于 [^0-9]。
      \f	匹配一个换页符。等价于 \x0c 和 \cL。
      \n	匹配一个换行符。等价于 \x0a 和 \cJ。
      \r	匹配一个回车符。等价于 \x0d 和 \cM。
      \s	匹配任何空白字符，包括空格、制表符、换页符等等。等价于 [ \f\n\r\t\v]。
      \S	匹配任何非空白字符。等价于 [^ \f\n\r\t\v]。
      \t	匹配一个制表符。等价于 \x09 和 \cI。
      \v	匹配一个垂直制表符。等价于 \x0b 和 \cK。
      \w	匹配包括下划线的任何单词字符。等价于'[A-Za-z0-9_]'。
      \W	匹配任何非单词字符。等价于 '[^A-Za-z0-9_]'。
      \xn	匹配 n，其中 n 为十六进制转义值。十六进制转义值必须为确定的两个数字长。例如，'\x41' 匹配 "A"。'\x041' 则等价于 '\x04' & "1"。正则表达式中可以使用 ASCII 编码。
      \num	匹配 num，其中 num 是一个正整数。对所获取的匹配的引用。例如，'(.)\1' 匹配两个连续的相同字符。
      \n	标识一个八进制转义值或一个向后引用。如果 \n 之前至少 n 个获取的子表达式，则 n 为向后引用。否则，如果 n 为八进制数字 (0-7)，则 n 为一个八进制转义值。
      \nm	标识一个八进制转义值或一个向后引用。如果 \nm 之前至少有 nm 个获得子表达式，则 nm 为向后引用。如果 \nm 之前至少有 n 个获取，则 n 为一个后跟文字 m 的向后引用。如果前面的条件都不满足，若 n 和 m 均为八进制数字 (0-7)，则 \nm 将匹配八进制转义值 nm。
      \nml	如果 n 为八进制数字 (0-3)，且 m 和 l 均为八进制数字 (0-7)，则匹配八进制转义值 nml。
      \un	匹配 n，其中 n 是一个用四个十六进制数字表示的 Unicode 字符。例如， \u00A9 匹配版权符号 (?)。

## 运算符优先级
      正则表达式从左到右进行计算，并遵循优先级顺序，这与算术表达式非常类似。
      相同优先级的从左到右进行运算，不同优先级的运算先高后低。下表从最高到最低说明了各种正则表达式运算符的优先级顺序：
      运算符	描述
      \	转义符
      (), (?:), (?=), []	圆括号和方括号
      *, +, ?, {n}, {n,}, {n,m}	限定符
      ^, $, \任何元字符、任何字符	定位点和序列（即：位置和顺序）
      |	替换，"或"操作
      字符具有高于替换运算符的优先级，使得"m|food"匹配"m"或"food"。若要匹配"mood"或"food"，请使用括号创建子表达式，从而产生"(m|f)ood"。

      注意：^表示字符串的开头，但它还有另外一个含义。当在一组方括号里使用^是，它表示"非"或"排除"的意思，
               常常用来剔除某个字符。如:^[^0-9][0-9]$

## 修饰符
    修饰符放在第二个/后面（/\d+/修饰符），js支持三个修饰符：
    1、i：用以说明匹配是否区分大小写
    2、g：说明模式匹配应该是全局的，也就是找出被检索中所有的匹配。
    3、m：用以在多行模式中执行匹配。

## String对象的正则表达式匹配、检索、替换方法
  string对象支持4中正则表达式的方法：
  1、search（）：它的参数是一个正则表达式，返回第一个匹配的起始位置，如果没有找到返回-1。
  <script>
  var reg=/\d+/;
  console.log("hell,4dadf1245".search(reg));  //5
  </script>
  注意：如果search（）参数不是正则表达式，它会调用RegExp构造函数将其转换为正则表达式，在进行匹配。在search（）中不支持全局匹配（g）。

  2、replace（）：用以检索和替换操作。它有两个参数：第一个是正则表达式，第二个参数是要进行替换的字符串。
  <script>
  //只替换第一个匹配项
  console.log("hell,4dadf1245".replace(/\d/, "你"));    //hell,你dadf1245
      //全局检索，替换所有匹配项
  console.log("hell,4dadf1245".replace(/\d/g, "你"));    //hell,你dadf你你你你
  </script>
  3、match（）：它只有一个参数就是正则表达式，返回的是一个由匹配结构组成的数组，如果正则表达式设置了修饰符g，它返回的是所有匹配结果的数组。如果没有修饰符g，返回数组形式的第一个匹配项。
  <script>
  //只替换第一个匹配项
  console.log("hell,4dadf1245".match(/\d/, "你")); //[4]
      //全局检索，替换所有匹配项
  console.log("hell,4dadf1245".match(/\d/g, "你"));    //[4,1,2,4,5]
  </script>
          注意：当正则表达式中有用（）包裹起来的子项时，在使用match匹配时，它会先将整体匹配存入第一个元素中，然后依次将每个（）子项匹配的结果存入后续元素中。如下
  <script>
  var reg=/(\w+):\/\/([\w.]+)/;
  var url="https://www.bxjr.com";
  var result=url.match(reg);
  if(result){
  console.log(result[0]); //https://www.bxjr.com
  console.log(result[1]); //https
  console.log(result[2]); //www.bxjr.com
  }
  </script>
  注意：match分割成数组，不适用全局匹配g。


  4、split（）：方法参数也是一个正则表达式。


## RegExp对象

  RegExp构造函数带有两个字符串参数，第一个参数为正则表达式主体，第二个参数是正则表达式的修饰符（可选）只能传入g,i,m。
  <script>
  var reg=new RegExp("\\d{5}","g");
  console.log("11111".search(reg));
  </script>
  特别注意：1、在正则表达式构造函数中，不论是字符串直接量还是正则表达式，都使用“\"字符串作为转义符的前缀，所以在给RegExp（）传入一个字符串正则表达式时，必须将”\"替换成“\\"（如上）。
                 2、正则表达式构造函数接受的是两个字符串参数，故需要将参数用双引号括起来。

## RegExp的方法
  1、exec（）
  2、test（）：它的参数是一个字符串，用test（）对某个字符串进行检测，如果包含正则表达式的一个匹配结果，则返回true.
  <script>
  console.log(/\d/.test("12344"));    //true
  </script>







