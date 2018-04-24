# chaijs-guide

## 语言链：
下面的接口是单纯作为语言链提供以期提高断言的可读性。除非被插件改写否则它们一般不提供测试功能。<br />
to <br />
be <br />
been <br />
is <br />
that <br />
which <br />
and <br />
has <br />
have <br />
with <br />
at <br />
of <br />
same <br />
 <br />
## API:
.not
目标取反 <br />
// query的值不为true <br />
expect(query('d', url)).to.not.be.equal(‘true’); <br />
 <br />
### 类型判断
.a(type)/.an(type) <br />
既可作为语言链，又可作为断言使用 <br />
type: string,被测试的值的类型 <br />
// 断言 <br />
expect(‘test’).to.be.a(‘string’); <br />
expect({foo: ‘bar’}).to.be.a(‘object); <br />
expect(null).to.be.a(‘null); <br />
expect(undefined).to.be.a(‘undefined’); <br />
expect(new Error).to.be.a(‘error’); <br />
expect(new Promise).to.be.a(‘promise’); <br />
// 语言链 <br />
expect(foo).to.be.a.instanceof(Foo); <br />
 <br />
.ok <br />
目标为真值 <br />
expect(1).to.be.ok; <br />
expect(null).to.not.be.ok; <br />
 <br />
.true <br />
目标为true（不进行类型转换） <br />
expect(true).to.be.true; <br />
expect(1).to.not.be.ok; <br />
 <br />
.false <br />
目标为false <br />
expect(false).to.be.false; <br />
expect(0).to.not.be.false; <br />
 <br />
.null <br />
目标为null <br />
expect(null).to.be.null; <br />
expect(undefined).to.not.be.null; <br />
 <br />
.undefined <br />
目标为undefined <br />
expect(undefined).to.be.undefined; <br />
expect(null).to.not.be.undefined; <br />
 <br />
.NaN <br />
目标为非数字NaN <br />
expect(‘foo’).to.be.NaN; <br />
expect(4).to.not.be.NaN; <br />
 <br />
.arguments <br />
目标为一个参数对象argument <br />
expect(argument).to.be.argument; <br />
 <br />
.instanceof(constructor) <br />
constructor: Constructor, 构造函数 <br />
断言目标为一个构造函数constructor的一个实例 <br />
var Tea = function (name) { this.name = name }, <br />
  Chai = new Tea('chai') <br />
 <br />
expect(Chai).to.be.an.instanceof(Tea) <br />
expect([1, 2, 3]).to.be.an.instanceof(Array) <br />
 <br />
 <br />
### 大小判断
.equal(value) <br />
目标=== value，如果设置了deep标记，则目标深度等于value <br />
expect(‘hello’).to.equal(‘hello’); <br />
expect(42).to.equal(42); <br />
expect(1).to.not.equal(true); <br />
expect({ foo: ‘bar’ }).to.not.equal({ foo: ‘bar’ }); <br />
expect({ foo: ‘bar’ }).to.deep.equal({ foo: ‘bar’ }); <br />
 <br />
.eql(value) <br />
目标深度等于value，相当于deep.equal(value)； <br />
expect({ foo: ‘bar’ }).to.eql({ foo: ‘bar’ }); <br />
 <br />
.above(value) <br />
value: Number <br />
目标大于value; <br />
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。 <br />
expect(10).to.be.above(2); <br />
expect(‘foo’).to.have.length.above(2); <br />
expect([1,2,3]).to.have.length.above(2); <br />
 <br />
.least(value) <br />
value: Number <br />
目标大于等于value; <br />
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。 <br />
expect(10).to.be.at.least(10); <br />
expect(‘foo’).to.have.length.of.at.least(3); <br />
expect([1,2,3]).to.have.length.of.at.least(3); <br />
 <br />
.below(value) <br />
value: Number <br />
目标小于value; <br />
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。 <br />
expect(10).to.be.below(11); <br />
expect(‘foo’).to.have.length.below(4); <br />
expect([1,2,3]).to.have.length.below(4); <br />
 <br />
.most(value) <br />
value: Number <br />
目标小于或等于value; <br />
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。 <br />
expect(10).to.be.at.most(10); <br />
expect(‘foo’).to.have.length.of.at.most(4); <br />
expect([1,2,3]).to.have.length.of.at.most(3); <br />
 <br />
.within(start, finish) <br />
start: Number, 下限 <br />
finish: Number, 上限 <br />
目标小于或等于value; <br />
也可接在length后断言一个最小的长度。相比直接提供长度的好处是提供了更详细的错误消息。 <br />
expect(7).to.be.within(5, 10); <br />
expect(‘foo’).to.have.length.within(2, 4); <br />
expect([1,2,3]).to.have.length.within(2, 4); <br />
 <br />
 <br />
### 长度判断
.exist <br />
目标存在（非null也非undefined） <br />
var foo = ‘hi’, <br />
   bar = null, <br />
   baz; <br />
expect(foo).to.exist; <br />
expect(bar).to.not.exist; <br />
expect(baz).to.not.exist; <br />
 <br />
.empty <br />
目标长度为0。对于数组和字符串，它检查length属性，对于对象，它检查可枚举属性的数量。 <br />
expect([]).to.be.empty; <br />
expect(‘’).to.be.empty; <br />
expect({}).to.be.empty; <br />
 <br />
.length <br />
设置.have.length标记作为比较length属性值的前缀 <br />
expect('foo').to.have.length.above(2) <br />
expect([1, 2, 3]).to.have.length.within(2, 4) <br />
 <br />
.lengthOf(value) <br />
value: Number <br />
断言目标的length属性为期望的值 <br />
expect([1, 2, 3]).to.have.lengthOf(3) <br />
expect('foobar').to.have.lengthOf(6) <br />
 <br />
 <br />
### 从属关系
.deep <br />
设置deep标记，然后使用equal和property断言。该标记可以让其后的断言不是比较对象本身，而是递归比较对象的键值对。 <br />
expect(foo).to.deep.equal({ bar: 'baz'}) <br />
expect({ foo: { bar: { baz: 'quux'}}}).to.have.deep.property('foo.bar.baz', 'quux') <br />
Deep.property中的特殊符号可以使用双反斜杠进行转义（第一个反斜杠是在字符串参数中对第二个反斜杠进行转义，第二个反斜杠用于在property中进行转义） <br />
var deepCss = { '.link': { '[target]': 42 } } <br />
expect(deepCss).to.have.deep.property('\\.link.\\[target\\]', 42) <br />
 <br />
.any <br />
至少包含一个；在keys断言之前使用any标记（与all相反）。 <br />
expect(foo).to.have.any.keys('bar', 'baz') <br />
 <br />
.all <br />
全部包含；在keys断言之前使用all标记（与any相反）。 <br />
expect(foo).to.have.all.keys('bar', 'baz') <br />
 <br />
.match(regexp) <br />
regexp: RegExp, 正则表达式 <br />
断言目标匹配到一个正则表达式。 <br />
expect('foobar').to.match(/^foo/) <br />
 <br />
.string(string) <br />
string: String, 字符串 <br />
断言目标字符串包含另一个字符串。 <br />
expect('foobar').to.have.string('bar') <br />
 <br />
.keys(key1, [key2], [...]) <br />
key: String | Array | Object 属性名 <br />
断言目标包含传入的属性名。与any，all，contains或者have前缀结合使用会影响测试结果： <br />
当与any结合使用时，无论是使用have还是使用contains前缀，目标必须至少存在一个传入的属性名才能通过测试。注意，any或者all应当至少使用一个，否则默认为all <br />
当结合all和contains使用时，目标对象必须至少拥有全部传入的属性名，但是它也可以拥有其它属性名 <br />
当结合all和have使用时，目标对象必须且仅能拥有全部传入的属性名 <br />
// 结合any使用 <br />
expect({ foo: 1, bar: 2, baz: 3 }).to.have.any.keys('foo', 'bar') <br />
expect({ foo: 1, bar: 2, baz: 3 }).to.contains.any.keys('foo', 'bar') <br />
// 结合all使用 <br />
expect({ foo: 1, bar: 2, baz: 3 }).to.have.all.keys('foo', 'bar', 'baz') <br />
expect({ foo: 1, bar: 2, baz: 3 }).to.contains.all.keys('foo', 'bar') <br />
// 传入string <br />
expect({ foo: 1, bar: 2, baz: 3 }).to.have.any.keys('foo')// 传入Array <br />
expect({ foo: 1, bar: 2, baz: 3 }).to.have.all.keys(['foo', 'bar', 'baz'])// 传入Object <br />
expect({ foo: 1, bar: 2, baz: 3 }).to.have.any.keys({ bar: 2, foo: 1 }) <br />
 <br />
.include(value)/contains(value) <br />
value: Object | String | Number <br />
include()和contains()即可作为属性类断言前缀语言链又可作为作为判断数组、字符串是否包含某值的断言使用。当作为语言链使用时，常用于key()断言之前。 <br />
expect([1, 2, 3]).to.include(2) <br />
expect('foobar').to.include('bar') <br />
expect({ foo: 'bar', hello: 'universe' }).to.include.keys('foo') <br />
 <br />
.property(name, [value]) <br />
name: String，属性名 <br />
value: Mixed，可选，属性值 <br />
断言目标是否拥有某个名为name的属性，可选地如果提供了value则该属性值还需要严格等于（===）value。如果设置了deep标记，则可以使用点.和中括号[]来指向对象和数组中的深层属性。 <br />
// 简单引用var obj = { foo: 'bar' } <br />
expect(obj).to.have.property('foo') <br />
expect(pbj).to.have.property('foo', 'bar') <br />
// 深层引用var deepObj = { <br />
  green: { tea: 'matcha' }, <br />
  teas: [ 'Chai', 'matcha', { tea: 'konacha' } ] <br />
} <br />
 <br />
expect(deepObj).to.have.deep.property('green.tea', 'matcha') <br />
expect(deepObj).to.have.deep.property('teas[1]', 'matcha') <br />
expect(deepObj).to.have.deep.property('teas[2].tea', 'konacha') <br />
 <br />
如果目标是一个数组，还可以直接使用一个或多个数组下标作为name来在嵌套数组中断言deep.property <br />
 <br />
var arr = [ <br />
  [ 'chai', 'matcha', 'konacha' ], <br />
  [ { tea: 'chai' }, <br />
    { tea: 'matcha' }, <br />
    { tea: 'konacha' } <br />
  ] <br />
] <br />
expect(arr).to.have.deep.property('[0][1]', 'matcha') <br />
expect(arr).to.have.deep.property('[1][2].tea', 'konacha') <br />
 <br />
此外，property把断言的主语（subject）从原来的对象变为当前属性的值，使得可以在其后进一步衔接其他链式断言（来针对这个属性值进行测试） <br />
expect(obj).to.have.property('foo')
  .that.is.a('string') <br />
expect(deepObj).to.have.property('green')
  .that.is.an('object')
  .that.deep.equals({ tea: 'matcha' }) <br />
expect(deepObj).to.have.property('teas')
  .that.is.an('array')
  .with.deep.property('[2]')
    .that.deep.equals({ tea: 'konacha' }) <br />
注意，只有当设置了deep标记的时候，在property() name中的点（.）和中括号（[]）才必须使用双反斜杠\进行转义（为什么是双反斜杠，在前文有提及），当没有设置deep标记的时候，是不能进行转义的 <br />
// 简单指向var css = { '.link[target]': 42 } <br />
expect(css).to.have.property('.link[target]', 42) <br />
//深度指向var deepCss = { 'link': { '[target]': 42 } } <br />
expect(deepCss).to.have.deep.property('\\.link\\.[target]', 42) <br />
 <br />
.ownProperty(name) <br />
name: String, 属性名 <br />
断言目标拥有名为name的自有属性 <br />
expect('test').to.have.ownProperty('length') <br />
 <br />
.ownPropertyDescription(name[, descriptor]) <br />
name: String, 属性名 <br />
descriptor: Object, 描述对象，可选 <br />
断言目标的某个自有属性存在描述符对象，如果给定了descroptor描述符对象，则该属性的描述符对象必须与其相匹配 <br />
expect('test').to.have.ownPropertyDescriptor('length') <br />
expect('test').to.have.ownPropertyDescriptor('length', {
  enumerable: false,
  configrable: false,
  writeable: false,
  value: 4
}) <br />
expect('test').not.to.have.ownPropertyDescriptor('length', {
  enumerable: false,
  configurable: false,
  writeable: false,
  value: 3
})// 将断言的主语改为了属性描述符对象 <br />
expect('test').to.have.ownPropertyDescriptor('length')
  .to.have.property('enumerable', false) <br />
expect('test').to.have.ownPropertyDescriptor('length')
  .to.have.keys('value') <br />


