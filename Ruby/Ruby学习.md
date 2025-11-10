1.ruby方法的返回值通常是方法中最后一个表达式的值，如果最后一个表达式的值不存在，则方法返回的值为nil。也可以采用return语句返回一个或多个返回值。
如：

    def test
        i = 100
        j = 200
        k = 300
    return i, j, k
    end


2.单引号''：

	字符串中的内容按字面值处理
	不会对特殊字符如（\n）进行转义
	不能插入变量

双引号"":

	支持转义字符
	支持字符串插值


3.to_s和to_str
to_i和to_int

puts：
    
    当把一个对象最为参数传递给puts()方法的时候，puts()方法会立即自动隐式地调用对象的to_s()方法将对象转换为字符串，字符串对象除外。

p：
    
    p会隐式地调用inspect方法。inspect方法把一个对象表示为字符串，在需要的时候，还能直接从字符串还原回对象。

gets：
    
    ruby中gets会接受输入的一切
    如：age = gets
        puts "I am " + age + "years old."
        则会输出I am 18
               years old.

gets.chomp()：

    chomp()会移除字符串尾部的分离符

    


4.块的定义
ruby块是一段代码，它可以作为参数传递给方法，并在方法内部执行。
块通常用于迭代、回调、异步处理等功能。
与函数或方法不同，块不是独立的对象，不能单独存在，必须附着在方法调用上。

块可以通过两种方式定义：
	do...end
	{...}


5.ruby中如何确定数据类型
puts a.class	#即可输出对象a的类型


6.numbers = [1, 2, 3, 4]
puts numbers.inject(:+)		#输出10
puts numbers.inject(9, :+) 	#输出19
puts numbers.inject(:*)		#输出24
puts numbers.inject(9, :*)	#输出216


7.puts nil || 12		#输出12


8.
..闭区间
puts (1..5).to_a		#输出1 2 3 4 5

...左闭右开区间
puts (1...5).to_a 		#输出1 2 3 4


9.单引号和双引号和反引号
单引号所包含的内容不会做转义，直接就是字符串的内容。
puts 'hello world\n'	#会直接输出hello world\n


双引号中的内容首先会进行查找和替换转义符\
其次对表达式进行求值，对字符串中的#{expression}进行替换
所以
title1 = 'test\n'
title2 = "test\n"
puts "this is a #{title1}"	#输出this is a test\n
puts "this is a #{title2}"	#输出this is a test


反引号类似于命令行
puts `dir`	#会输出当前目录下的内容，等同于在命令行中使用dir


10.字符串
a = 'hello'
b = 'world'
puts a + ' ' + b
puts "#{a} #{b}"

puts a.length	#输出5
puts a.upcase	#输出HELLO
puts a.capitalize	#输出Hello
puts a.gsub('o', '')	#输出hell	#会替换所有匹配的字符，不只是第一个


11.变量赋值
a = 'hello world'
puts a.object_id	#输出60

a.replace('hell world')
puts a.object_id	#输出60

a = 'hello world'
puts a.object_id	#输出80


12.hash表

    a = {a: 1, b: 2}	#注意a:是连在一起的
    puts a[:a]	#输出1

    a = {"name" => "li", "age" => 36, "hobbies" => ["video game", "music"]}
    puts a["name"]	#输出li
    puts a.keys.to_s	#输出{"name", "age", "hobbies"}
    puts a.values.to_s	#输出{"li", 36, ["video game", "music"]}
    a.delete("hobbies")	
    puts a.to_s		#输出{"name" => "li", "age" => 36}
    a["cellphone"] = "123456"
    puts a.to_s		#输出{"name"=>"li", "age"=>36, "cellphone"=>"123456"}


13.以！结尾的方法会改变变量自身
a = "hello"
a.capitalize
puts a		#会输出hello
a.capitalize!
puts a		#会输出Hello


14.以？结尾的方法会返回true或false
a = "hello"
puts a.is_a?(String)	#会输出true


15.ruby中只有nil和false是假，其余均为真
a = nil
puts a.nil?	#会输出true

16.Array常用方法
a = [1, 2, "hello"]
puts a.length	#会输出3
puts a.size	#会输出3

puts a.first	#会输出1
puts a.last	#会输出hello

b = ["world"]
c = a + b
d = b * 3
e = c - a
这些方法并不会改变数组本身

a = []
a.push(1)	
a.push(2)
a.unshift(3)	#数组a [3, 1, 2]

a.pop		#数组a [3, 1]
a.shift		#数组a [1]

a = []
a << 3		#数组a [3]

a.concat([4, 5])	#数组a [3, 4, 5]
a.delete(1)	#会删掉数组中所有为1的元素
这些方法会改变数组本身

a = [3, 4, 5]
a.index(4)	#返回元素4的位置
a[0] = 1	#数组a [1, 4, 5]
a.max
a.min

拆分数组
a = [1, 2, 3]
b, c = a	#b = 1, c = 2
b, *c = a	#b = 1, c = [2, 3]


17.symbol是字符串String的一种


18.ruby中的Method

参数设置默认值
def function(name="Leon")
	puts "Hi " + name
end
function	#如果不给参数，则会输出Hi Leon

ruby中区分不同的方法只通过方法名，同名方法会被覆盖。

方法返回值
	方法中的最后一行代码的返回值默认会作为方法的返回值
	也可以显式地使用return关键字


19.ruby中的Block
Block类似于一个方法，可以使用do和end 或 {}来定义

Block内置方法

a = [1, 2, 3]
a.each do |x|
  puts x
end


a = {"a" => 1, "b" => 2}
a.each do |key , value|
  puts key
end


20.逻辑运算符的优先级

&&  >  ||  >  = += -=  >  not  >  and or


21.全局变量 $开头
对象实例属性 @开头
类属性 @@开头
常亮 大写字母开头

22.block和proc
block就是proc，但是不能独立存在，不能赋值给变量，但是proc可以，所以block是一次性的proc。

    p1 = proc {puts "good morning"}
    p2 = proc {puts "good afternoon"}

23.lambda
lambda是特殊的proc

    l = lambda { |X| puts x} 

24.ruby gem类似于java的jar包或者c的库

bundle:一个Rails环境实际上是一系列gem包组成，可以通过gem list来查看所有的gem版本。bundle可以明确一个工程所依赖的包的版本。


