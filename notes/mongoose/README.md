# mongoose 学习笔记

目录：

* [Schema](#Schema)
* [Model](#Model)
* [Entity](#Entity)
* [statics](#statics)
* [methods](#methods)
* [virtual](#virtual)
* [set](#set)
* [add](#add)
* [Query](#Query)
* [Population](#Population)
* [Validation](#Validation)
* [Middleware](#Middleware)
* [Plugins](#Plugins)

## Schema

-   简介

    一种以文件形式存储的数据库模型骨架，无法直接通往数据库端，也就是说它不具备对数据库的操作能力，仅仅
    只是数据库模型在程序片段中的一种表现，可以说是数据属性模型(传统意义的表结构)，又或着是“集合”的模
    型骨架。

    ```js
    var mongoose = require('mongoose');
    var TestSchema = new mongoose.Schema({
      name : { type:String },
      age  : { type:Number, default:0 },
      time : { type:Date, default:Date.now },
      email: { type:String}
    });
    ```

-   基本属性类型

    String, Number, Date, Buffer, Boolean, Mixed, Objectid, Array

    这些类型中，除了 Mixed、ObjectId 是 Schema.Types 的属性外，其它都是 javascript 自有的属性。

-   Mixed

    Schema.Types.Mixed是Mongoose定义的混合类型，该混合类型未定义具体形式。

    如果未定义具体内容，可以直接使用{}来定义，以下两句等价

    ```js
    var AnySchema = new Schema({any:{}});
    var AnySchema = new Schema({any:Schema.Types.Mixed});
    ```

    混合类型因为没有特定约束，因此可以任意修改，一旦修改了原型，则必须调用markModified()

    ```js
    person.anything = {x:[3,4,{y:'change'}]}
    person.markModified('anything');//传入anything，表示该属性类型发生变化
    person.save();
    ```

-   ObjectId

    一种特殊而且非常重要的类型，每个Schema都会默认配置这个属性，属性名为_id，
    除非自己定义，方可覆盖。该类型的值由系统自己生成，从某种意义上几乎不会重复。

-   Array

    Array在JavaScript编程语言中并不是数组，而是集合，因此里面可以存入不同的值，以下代码等价：

    ```js
    var ExampleSchema1 = new Schema({array:[]});
    var ExampleSchema2 = new Schema({array:Array});
    var ExampleSchema3 = new Schema({array:[Schema.Types.Mixed]});
    var ExampleSchema4 = new Schema({array:[{}]});
    ```

## Model

由Schema构造生成的模型，除了 Schema 定义的数据库骨架以外，还具有数据库操作的行为，类似于管
理数据库属性、行为的类。

```js
var db = mongoose.connect('mongodb://127.0.0.1:27017/test');
var TestModel = db.model('TestModel', TestSchema);
```

## Entity

由Model创建的实体，使用save方法保存数据，Model和Entity都有能影响数据库的操作，但 Model
比Entity更具操作性。

```js
var TestEntity = new TestModel({
  name : 'Lenka',
  age  : 36,
  email: 'lenka@qq.com'
});
console.log(TestEntity.name); // Lenka
console.log(TestEntity.age); // 36
```

## statics

静态方法

```js
PersonSchema.statics.findByName = function(name,cb){
  this.find({name:new RegExp(name,'i'),cb});
}
```
```js
var PersonModel = mongoose.model('Person',PersonSchema);
PersonModel.findByName('krouky',function(err,persons){
  //找到所有名字包含krouky的人
});
```

## methods

成员方法

```js
var PersonSchema = new Schema({name:String,type:String});

PersonSchema.methods.findSimilarTypes = function(cb){
  return this.model('Person').find({type:this.type},cb);
}
```
```js
var PersonModel = mongoose.model('Person',PersonSchema);

var krouky = new PersonSchema({name:'krouky',type:'前端工程师'});

krouky.findSimilarTypes(function(err,persons){
  //persons中就能查询到其他前端工程师
});
```

## virtual

虚拟属性

```js
var PersonSchema = new Schema({
  first_name: {type: String},
  last_name: {type: String},
});

var PersonModel = mongoose.model('Person',PersonSchema);
```
```js
PersonSchema.virtual('full_name').get(function(){
  return this.first_name + ' ' + this.last_name;
});
```
```js
PersonSchema.virtual('full_name').set(function(full_name){
  var split = full_name.split(' ');
  this.first_name = split[0];
  this.last_name = split[1];
});
```

这样可以使用 full_name 来调用全名了：

```js
var mvp = new PersonModel({
  first_name: 'Kobe',
  last_name: 'Bryant'
});

console.log(mvp.full_name); // Kobe Bryant
```

反之如果知道 full_name ，也可以反解 first_name 和 last_name 属性：

```js
var mvp = new PersonModel();
mvp.full_name = 'Kobe Bryant';

console.log(mvp.first_name); // Kobe
console.log(mvp.last_name);  // Bryant
```

## set

在使用new Schema()时，可以追加一个参数 options 来配置Schema的配置，形如：

```js
var ExampleSchema = new Schema({
  // ...
}, options);
```

或者使用 set 方法

```js
var ExampleSchema = new Schema({

});

ExampleSchema.set(option,value);
```

可供配置项有：

```
safe              安全模式（默认 true ）
strict            严格配置（默认 true ）
shardKey          需要mongodb做分布式，才会使用该选项
capped            如果有数据库的批量操作，该属性能限制一次操作的量
versionKey        版本锁是Mongoose默认配置（__v属性）的，如果你想自己定制
autoIndex         自动索引
```

## add

动态增加字段

```js
UserSchema.add({
  last_modified: {type: Date },
})
```

## Query

With a JSON doc

```js
Person.
  find({
    occupation: /host/,
    'name.last': 'Ghost',
    age: { $gt: 17, $lt: 66 },
    likes: { $in: ['vaporizing', 'talking'] }
  }).
  limit(10).
  sort({ occupation: -1 }).
  select({ name: 1, occupation: 1 }).
  exec(callback);
```

Using query builder

```js
Person.
  find({ occupation: /host/ }).
  where('name.last').equals('Ghost').
  where('age').gt(17).lt(66).
  where('likes').in(['vaporizing', 'talking']).
  limit(10).
  sort('-occupation').
  select('name occupation').
  exec(callback);
```

模糊查询

```js
var condition = {
  $or:[
    {user_name: {$regex: keywords, $options: 'i'}},
    {product_name: {$regex: keywords, $options: 'i'}},
  ]
}
```

## Population

-   基础

    ```js
    ProductSchema = new Schema({
      user_id: {
        type: Schema.ObjectId,
        ref: 'UserModel'
      },
    });

    var ProductModel = mongoose.model('ProductModel',ProductSchema);
    ```
    ```js
    ProductModel.findOne().populate('user_id').exec(function (err, data){
      console.log(data.user_id);
    });
    ```

-   只取出部分字段

    ```js
    .populate('user_id', 'user_name') // only return the user's name
    ```

-   关联多个表，可以连续使用多个 populate

    ```js
    .populate('user_id').populate('stockroom_id')
    ```
    ```
    .populate('user_id stockroom_id') // space delimited path names
    ```

-   查询条件和其它选项

    ```js
    var mongoose = require('mongoose')
      , Schema = mongoose.Schema

    var personSchema = Schema({
      _id     : Number,
      name    : String,
      age     : Number,
      stories : [{ type: Schema.Types.ObjectId, ref: 'Story' }]
    });

    var storySchema = Schema({
      _creator : { type: Number, ref: 'Person' },
      title    : String,
      fans     : [{ type: Number, ref: 'Person' }]
    });

    var Story  = mongoose.model('Story', storySchema);
    var Person = mongoose.model('Person', personSchema);
    ```
    ```js
    Story
      .find(...)
      .populate({
        path: 'fans',
        match: { age: { $gte: 21 }},
        select: 'name -_id',
        options: { limit: 5 }
      })
      .exec()
    ```

-   多键嵌套

    ```js
    var userSchema = new Schema({
      name: String,
      friends: [{ type: ObjectId, ref: 'User' }]
    });
    ```
    ```js
    User
      .findOne({ name: 'Val' })
      .populate({
        path: 'friends',
        // Get friends of friends - populate the 'friends' array for every friend
        populate: { path: 'friends' }
      });
    ```

-   跨越数据库

    ```js
    var eventSchema = new Schema({
      name: String,
      // The id of the corresponding conversation
      // Notice there's no ref here!
      conversation: ObjectId
    });
    var conversationSchema = new Schema({
      numMessages: Number
    });
    ```
    ```js
    var db1 = mongoose.createConnection('localhost:27000/db1');
    var db2 = mongoose.createConnection('localhost:27001/db2');

    var Event = db1.model('Event', eventSchema);
    var Conversation = db2.model('Conversation', conversationSchema);
    ```
    ```js
    Event
      .find()
      .populate({ path: 'conversation', model: Conversation })
      .exec(function(error, docs) { /* ... */ });
    ```

## Validation

验证器

```js
required      非空验证
min/max       范围验证（边值验证）
enum/match    枚举验证/匹配验证
validate      自定义验证规则
```

示例

```js
var PersonSchema = new Schema({
  name:{
    type:'String',
    required:true //姓名非空
  },
  age:{
    type:'Nunmer',
    min:18,       //年龄最小18
    max:120     //年龄最大120
  },
  city:{
    type:'String',
    enum:['北京','上海']  //只能是北京、上海人
  },
  phone: {
    type: String,
    validate: {
      validator: function(v) {
        return /d{3}-d{3}-d{4}/.test(v);
      },
      message: '{VALUE} is not a valid phone number!'
    }
  }
});

var Person = mongoose.model('Person', PersonSchema);

var p = new Person();

p.phone = '555.0123';
// Prints 'ValidationError: 555.0123 is not a valid phone number!'
console.log(p.validateSync().toString());

p.phone = '201-555-0123';
// Prints undefined - validation succeeded!
console.log(p.validateSync());
```
```js
var toySchema = new Schema({
  color: String,
  name: String
});

var Toy = mongoose.model('Toy', toySchema);

Toy.schema.path('color').validate(function (value) {
  return /blue|green|white|red|orange|periwinkle/i.test(value);
}, 'Invalid color');

var toy = new Toy({ color: 'grease'});

toy.save(function (err) {
  // err is our ValidationError object
  // err.errors.color is a ValidatorError object

  console.log(err.errors.color.message) // prints 'Validator 'Invalid color' failed for path color with value `grease`'
  console.log(String(err.errors.color)) // prints 'Validator 'Invalid color' failed for path color with value `grease`'
  console.log(err.errors.color.kind)  // prints 'Invalid color'
  console.log(err.errors.color.path)  // prints 'color'
  console.log(err.errors.color.value) // prints 'grease'
  console.log(err.name) // prints 'ValidationError'
  console.log(err.message) // prints 'Validation failed'
});
```

## Middleware

中间件

pre 方法表示在执行操作之前，先执行回调函数

```js
UserSchema.pre('save', function (next) {
  this.last_modified = new Date
  next()
})
```

post方法表示在执行操作之后，再执行回调函数

```js
schema.post('find', function(result) {
  console.log(this instanceof mongoose.Query); // true
  // prints returned documents
  console.log('find() returned ' + JSON.stringify(result));
  // prints number of milliseconds the query took
  console.log('find() took ' + (Date.now() - this.start) + ' millis');
});
```

## Plugins

插件

```js
// lastMod.js
module.exports = exports = function lastModifiedPlugin (schema, options) {
  schema.add({ lastMod: Date })

  schema.pre('save', function (next) {
    this.lastMod = new Date
    next()
  })

  if (options && options.index) {
    schema.path('lastMod').index(options.index)
  }
}
```
```js
// game-schema.js
var lastMod = require('./lastMod');
var Game = new Schema({ ... });
Game.plugin(lastMod, { index: true });
```
```js
// player-schema.js
var lastMod = require('./lastMod');
var Player = new Schema({ ... });
Player.plugin(lastMod);
```
