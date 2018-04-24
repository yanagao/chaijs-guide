# chaijs-guide

## 语言链：
下面的接口是单纯作为语言链提供以期提高断言的可读性。除非被插件改写否则它们一般不提供测试功能。
to
be
been
is
that
which
and
has
have
with
at
of
same

## API:
.not
目标取反
// query的值不为true
expect(query('d', url)).to.not.be.equal(‘true’);

类型判断
.a(type)/.an(type)
既可作为语言链，又可作为断言使用
type: string,被测试的值的类型
// 断言
expect(‘test’).to.be.a(‘string’);
expect({foo: ‘bar’}).to.be.a(‘object);
expect(null).to.be.a(‘null);
expect(undefined).to.be.a(‘undefined’);
expect(new Error).to.be.a(‘error’);
expect(new Promise).to.be.a(‘promise’);
// 语言链
expect(foo).to.be.a.instanceof(Foo);

.ok
目标为真值
expect(1).to.be.ok;
expect(null).to.not.be.ok;

.true
目标为true（不进行类型转换）
expect(true).to.be.true;
expect(1).to.not.be.ok;

.false
目标为false
expect(false).to.be.false;
expect(0).to.not.be.false;

.null
目标为null
expect(null).to.be.null;
expect(undefined).to.not.be.null;

.undefined
目标为undefined
expect(undefined).to.be.undefined;
expect(null).to.not.be.undefined;

.NaN
目标为非数字NaN
expect(‘foo’).to.be.NaN;
expect(4).to.not.be.NaN;

.arguments
目标为一个参数对象argument
expect(argument).to.be.argument;

.instanceof(constructor)
constructor: Constructor, 构造函数
断言目标为一个构造函数constructor的一个实例
var Tea = function (name) { this.name = name },
  Chai = new Tea('chai')

expect(Chai).to.be.an.instanceof(Tea)
expect([1, 2, 3]).to.be.an.instanceof(Array)


大小判断
.equal(value)
目标=== value，如果设置了deep标记，则目标深度等于value
expect(‘hello’).to.equal(‘hello’);
expect(42).to.equal(42);
expect(1).to.not.equal(true);
expect({ foo: ‘bar’ }).to.not.equal({ foo: ‘bar’ });
expect({ foo: ‘bar’ }).to.deep.equal({ foo: ‘bar’ });

.eql(value)
目标深度等于value，相当于deep.equal(value)；
expect({ foo: ‘bar’ }).to.eql({ foo: ‘bar’ });

.above(value)
value: Number
目标大于value;
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。
expect(10).to.be.above(2);
expect(‘foo’).to.have.length.above(2);
expect([1,2,3]).to.have.length.above(2);

.least(value)
value: Number
目标大于等于value;
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。
expect(10).to.be.at.least(10);
expect(‘foo’).to.have.length.of.at.least(3);
expect([1,2,3]).to.have.length.of.at.least(3);

.below(value)
value: Number
目标小于value;
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。
expect(10).to.be.below(11);
expect(‘foo’).to.have.length.below(4);
expect([1,2,3]).to.have.length.below(4);

.most(value)
value: Number
目标小于或等于value;
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。
expect(10).to.be.at.most(10);
expect(‘foo’).to.have.length.of.at.most(4);
expect([1,2,3]).to.have.length.of.at.most(3);

.within(start, finish)
start: Number, 下限
finish: Number, 上限
目标小于或等于value;
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。
expect(7).to.be.within(5, 10);
expect(‘foo’).to.have.length.within(2, 4);
expect([1,2,3]).to.have.length.within(2, 4);


长度判断
.exist
目标存在（非null也非undefined）
var foo = ‘hi’,
   bar = null,
   baz;
expect(foo).to.exist;
expect(bar).to.not.exist;
expect(baz).to.not.exist;

.empty
目标长度为0。对于数组和字符串，它检查length属性，对于对象，它检查可枚举属性的数量。
expect([]).to.be.empty;
expect(‘’).to.be.empty;
expect({}).to.be.empty;

.length
设置.have.length标记作为比较length属性值的前缀
expect('foo').to.have.length.above(2)
expect([1, 2, 3]).to.have.length.within(2, 4)

.lengthOf(value)
value: Number
断言目标的length属性为期望的值
expect([1, 2, 3]).to.have.lengthOf(3)
expect('foobar').to.have.lengthOf(6)


从属关系
.deep
设置deep标记，然后使用equal和property断言。该标记可以让其后的断言不是比较对象本身，而是递归比较对象的键值对。
expect(foo).to.deep.equal({ bar: 'baz'})
expect({ foo: { bar: { baz: 'quux'}}}).to.have.deep.property('foo.bar.baz', 'quux')
Deep.property中的特殊符号可以使用双反斜杠进行转义（第一个反斜杠是在字符串参数中对第二个反斜杠进行转义，第二个反斜杠用于在property中进行转义）
var deepCss = { '.link': { '[target]': 42 } }
expect(deepCss).to.have.deep.property('\\.link.\\[target\\]', 42)

.any
至少包含一个；在keys断言之前使用any标记（与all相反）。
expect(foo).to.have.any.keys('bar', 'baz')

.all
全部包含；在keys断言之前使用all标记（与any相反）。
expect(foo).to.have.all.keys('bar', 'baz')

.match(regexp)
regexp: RegExp, 正则表达式
断言目标匹配到一个正则表达式。
expect('foobar').to.match(/^foo/)

.string(string)
string: String, 字符串
断言目标字符串包含另一个字符串。
expect('foobar').to.have.string('bar')

.keys(key1, [key2], [...])
key: String | Array | Object 属性名
断言目标包含传入的属性名。与any，all，contains或者have前缀结合使用会影响测试结果：
当与any结合使用时，无论是使用have还是使用contains前缀，目标必须至少存在一个传入的属性名才能通过测试。注意，any或者all应当至少使用一个，否则默认为all
当结合all和contains使用时，目标对象必须至少拥有全部传入的属性名，但是它也可以拥有其它属性名
当结合all和have使用时，目标对象必须且仅能拥有全部传入的属性名
// 结合any使用
expect({ foo: 1, bar: 2, baz: 3 }).to.have.any.keys('foo', 'bar')
expect({ foo: 1, bar: 2, baz: 3 }).to.contains.any.keys('foo', 'bar')
// 结合all使用
expect({ foo: 1, bar: 2, baz: 3 }).to.have.all.keys('foo', 'bar', 'baz')
expect({ foo: 1, bar: 2, baz: 3 }).to.contains.all.keys('foo', 'bar')
// 传入string
expect({ foo: 1, bar: 2, baz: 3 }).to.have.any.keys('foo')// 传入Array
expect({ foo: 1, bar: 2, baz: 3 }).to.have.all.keys(['foo', 'bar', 'baz'])// 传入Object
expect({ foo: 1, bar: 2, baz: 3 }).to.have.any.keys({ bar: 2, foo: 1 })

.include(value)/contains(value)
value: Object | String | Number
include()和contains()即可作为属性类断言前缀语言链又可作为作为判断数组、字符串是否包含某值的断言使用。当作为语言链使用时，常用于key()断言之前。
expect([1, 2, 3]).to.include(2)
expect('foobar').to.include('bar')
expect({ foo: 'bar', hello: 'universe' }).to.include.keys('foo')

.property(name, [value])
name: String，属性名
value: Mixed，可选，属性值
断言目标是否拥有某个名为name的属性，可选地如果提供了value则该属性值还需要严格等于（===）value。如果设置了deep标记，则可以使用点.和中括号[]来指向对象和数组中的深层属性。
// 简单引用var obj = { foo: 'bar' }
expect(obj).to.have.property('foo')
expect(pbj).to.have.property('foo', 'bar')
// 深层引用var deepObj = {
  green: { tea: 'matcha' },
  teas: [ 'Chai', 'matcha', { tea: 'konacha' } ]
}

expect(deepObj).to.have.deep.property('green.tea', 'matcha')
expect(deepObj).to.have.deep.property('teas[1]', 'matcha')
expect(deepObj).to.have.deep.property('teas[2].tea', 'konacha')

如果目标是一个数组，还可以直接使用一个或多个数组下标作为name来在嵌套数组中断言deep.property

var arr = [
  [ 'chai', 'matcha', 'konacha' ],
  [ { tea: 'chai' },
    { tea: 'matcha' },
    { tea: 'konacha' }
  ]
]
expect(arr).to.have.deep.property('[0][1]', 'matcha')
expect(arr).to.have.deep.property('[1][2].tea', 'konacha')

此外，property把断言的主语（subject）从原来的对象变为当前属性的值，使得可以在其后进一步衔接其他链式断言（来针对这个属性值进行测试）
expect(obj).to.have.property('foo')
  .that.is.a('string')
expect(deepObj).to.have.property('green')
  .that.is.an('object')
  .that.deep.equals({ tea: 'matcha' })
expect(deepObj).to.have.property('teas')
  .that.is.an('array')
  .with.deep.property('[2]')
    .that.deep.equals({ tea: 'konacha' })
注意，只有当设置了deep标记的时候，在property() name中的点（.）和中括号（[]）才必须使用双反斜杠\进行转义（为什么是双反斜杠，在前文有提及），当没有设置deep标记的时候，是不能进行转义的
// 简单指向var css = { '.link[target]': 42 }
expect(css).to.have.property('.link[target]', 42)
//深度指向var deepCss = { 'link': { '[target]': 42 } }
expect(deepCss).to.have.deep.property('\\.link\\.[target]', 42)

.ownProperty(name)
name: String, 属性名
断言目标拥有名为name的自有属性
expect('test').to.have.ownProperty('length')

.ownPropertyDescription(name[, descriptor])
name: String, 属性名
descriptor: Object, 描述对象，可选
断言目标的某个自有属性存在描述符对象，如果给定了descroptor描述符对象，则该属性的描述符对象必须与其相匹配
expect('test').to.have.ownPropertyDescriptor('length')
expect('test').to.have.ownPropertyDescriptor('length', {
  enumerable: false,
  configrable: false,
  writeable: false,
  value: 4
})
expect('test').not.to.have.ownPropertyDescriptor('length', {
  enumerable: false,
  configurable: false,
  writeable: false,
  value: 3  
})// 将断言的主语改为了属性描述符对象
expect('test').to.have.ownPropertyDescriptor('length')
  .to.have.property('enumerable', false)
expect('test').to.have.ownPropertyDescriptor('length')
  .to.have.keys('value')


