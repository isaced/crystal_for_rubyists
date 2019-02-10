\newpage

# C��

�ܶ�C�ⶼ�����ã�����Ӧ�ó���������Ƕ�����ȥ��д���ǡ�
�� crystal ��,���� bindings ��ʹ���Ѵ��ڵ�C�ⳬ����,
��ʹ�� crystal ��������C��.����:crystal ʹ�� libpcre 
��ʵ���� Regex.������ Crystal �Լ����� libpcre ������:

```ruby
@[Link("pcre")]
lib LibPCRE
...
end
```

���� libpcre ��ֻ��Ҫ3�д���,����ʹ�� lib �ؼ�����������ͬһ����ķ��������ͷ�Ϊһ�顣

���Ҵ� Lib ��ʼ���C������������.

���������� fun �ؼ��ְ󶨵�C functions ��.

```ruby
@[Link("pcre")]
lib LibPCRE
  type Pcre = Void*
  fun compile = pcre_compile(pattern : UInt8*, options : Int, errptr : UInt8**, erroffset : Int*, tableptr : Void*) : Pcre
end
```

���������� matching ���Ͱ󶨵� libpcre �ı��� function �С���ˣ�
������ crystal ���������ɵػ�ȡ C function �ˡ�

```crystal
LibPCRE.compile(..)
```
