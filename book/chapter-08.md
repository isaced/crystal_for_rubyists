\newpage

# ������ܵ�

���ǵõ�һ�½���,��������һ�������� hello world.�ع�һ��:

```ruby
channel = Channel(String).new
10.times do
  spawn {
    channel.send "Hello?"
  }
  puts channel.receive
end
```

�� crystal �������ùؼ��� spawn ��һЩ���������û���������̵߳�����º�̨���С�
Ϊ�˴ﵽ������Ŀ��,spawn ������һ�������߳����� Fiber (��ά),���� fiber �ɱ��ͣ������������һ��������( core )�д��������� fiber.
Ok,��Ȼ���ǿ����� fiber ��̨���У������������Ҫ fiber �ķ���ֵ��.��ʱ���ܵ�( Channel )�������ó���


## Channel

����˼��,Channel ����һ�����շ������ͷ��Ĺܵ�,���� Channel ����ͨ�� send �� receive �����˴˽�����������һ��һ���ķ�������Ĵ���.

```ruby
channel = Channel(String).new
```

������ Channel(String).new ������һ���ܵ�,��Ҫע������������ڴ���һ������ send �� receive �ַ������͵���Ϣ�Ĺܵ���

```ruby
10.times do
  spawn {
    channel.send "Hello?"
  }
  puts channel.receive
end
```

�����Ȳ���ѭ�������������� spawn ����ܵ��������ݡ�����ܻ��ʡ�Ϊʲô����Ҫ�ں�̨�������ݡ�.
 send ������һ��������������������� main ��������ʹ�����ͻ���Զ�����������򡣿������:

```ruby
channel = Channel(String).new
channel.send "Hello?" # This blocks the program execution
puts channel.receive
```

����ĳ���������ʲô��?ʵ�����������û��ִ����,��Ϊ���� send ����������,������������֪����,����!


```ruby
spawn {
  channel.send "Hello?"
}
puts channel.receive
```

����ֻ���� spawn �ں�̨��ͨ���ܵ�������һ����Ϣ.Ȼ�������� channel.receive �������ķ���.�����������Ϣ�� ��hello?��,���Գ����ӡ hello? �����.