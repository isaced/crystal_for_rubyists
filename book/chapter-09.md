\newpage

# ���Ԫ���

����ϲ�� ruby ����Ϊ���Ķ�̬�Ժ�Ԫ��̣����Ǻ� ruby ��һ������,crystal ��һ�ֱ������ԣ���͵���������֮����һЩ�ؼ��Ե�����:

- û�� `eval`.
- û�� `send`.

�� crystal ��,����ʹ�� macro ���������������Ϊ��Ԫ���,����԰� macro �������δ���Ĵ��롣P.S.�����ڼ� macro ����չ���˴���.�����:

```ruby
macro define_method(name, content)
  def {{name}}
    {{content}}
  end
end

define_method foo, 1
# This generates:
#
#     def foo
#       1
#     end

foo # => 1
```

����������У����Ǵ�����һ�� macro ���� define_method.����ֻ�ǰ� macro ��Ϊһ����ͨ�ķ�����Ȼ�� macro �ͻᱻ��չ�ɣ�

```ruby
  def foo
    1
  end
```

�ᣡ���Ǿ�Ȼ�ڱ����ڼ�õ��� eval ��Ϊ��
Macro ��ǿ�󣬵�����һ�������㲻�ܴ���:

***һ�� macro Ӧ�ñ���չ��һ���Ϸ��� crystal ��Ŀ�С�***
