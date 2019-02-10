\newpage

# �����뷽������

Crystal �� ruby ���񣬵������� ruby ��

Crystal ��һ�־�̬�������ͺ����������ԡ������ʱ���㲻��ָ���������͡���Ϊ�������Լ����ƶϳ��������͡�

�ã���Ȼ��������ô����Ϊʲô��Ҫ����������?�����Ǵ���������ӿ�ʼ:

```ruby
def add(x, y)
  x + y
end

add 3, 5 # 8
```

�������Щ�� ruby ����һ����,����ֻ�Ƕ�����һ����������������͵ķ���,Ҫ������������һ�����ֺ��ַ����ĺ��أ�

```ruby
add 3, "Serdar"
```

���������� ruby ������һ��

```ruby
types.cr:2:in `+': String can't be coerced into Fixnum (TypeError)
	from types.cr:2:in `add'
	from types.cr:5:in `<main>'
```

�õ���һ�� typeError,�������ǲ����� ruby �й������Ͱ�����ʵ����һ�������ڼ����( runtime error ).��ζ����ĳ����������ڼ������

Ȼ�������� crystal ������һ��

    Error in ./types.cr:5: instantiating 'add(Int32, String)'

    add 3, "Serdar"
    ^~~

    in ./types.cr:2: no overload matches 'Int32#+' with types String
    Overloads are:
    - Int32#+(other : Int8)
    - Int32#+(other : Int16)
    - Int32#+(other : Int32)
    - Int32#+(other : Int64)
    - Int32#+(other : UInt8)
    - Int32#+(other : UInt16)
    - Int32#+(other : UInt32)
    - Int32#+(other : UInt64)
    - Int32#+(other : Float32)
    - Int32#+(other : Float64)
    - Int32#+()

    x + y
      ^

����,����������俴����ͦ���˵ģ�����ʵ�������Ǻ�ǿ�����ǵ� crystal ��Ȼû�б��뵫��Ȼ�������� crystal ��û�ж��ڡ�Int32#+()������������,
����������չʾ���������ܵ��������͡�crystal �����ֻ��ƾ��൱�����ǳ�˵�ġ������ڼ���󡱣���ζ�����ǵĴ���û�б���ɹ��������ڳ�������֮ǰ�Ͳ�׽���˴���

�������������һЩ�������Ͳ����ڷ��������Ƴ� number ����.

```ruby
def add(x : Number, y : Number)
  x + y
end

puts add 3, "Serdar"
```

����

    Error in ./types.cr:5: no overload matches 'add' with types Int32, String
    Overloads are:
    - add(x : Number, y : Number)

    puts add 3, "Serdar"
         ^~~

̫����,���ǵĳ�����һ��û�ܱ���ɹ�,����εĴ���������̺͸�׼ȷ������ֻ����x��y��ʹ�����������ơ�Crystal ���Ѿ���������������ֹ����ʹ�ô��ַ����ķ�����

## ��������


���Ǹղſ�����һЩ���أ�����������̸̸�������ء�
�������ؾ�����һЩ����֮����ֵ�һ��������Ȼ���ǿ���ӵ����ͬ�������ƣ��������ǵĲ���������ȴ��ͬ��������Щ����ʵ�����ǲ�ͬ�ġ�
�������������ǵ� add ����,������ɿ��Խ��� string ���͡�

```ruby
def add(x : Number, y : Number)
  x + y
end

def add(x: Number, y: String)
  x.to_s + y
end

puts add 3, 5

puts add 3, "Serdar"
```

Let's run it.

    $ crystal types.cr
    8
    3Serdar

���Ͼ���ʵ�ʲ����еķ������أ�crystal �ܹ��ֱ��������˵�Ĵ������ֵķ����ʹ����ַ����ķ��������𡣲����ܹ�����׼ȷ�ص������ǣ����ط����������ǲ������Ƶġ�
