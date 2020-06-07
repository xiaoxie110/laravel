# 在此处输入标题

标签（空格分隔）： 未分类

---
> 集合（Collection）Illuminate\Support\Collection 类了提供一个便捷的操作数组的封装。


### [创建一个新的集合](#创建一个新的集合)
 
```PHP
//collect 辅助函数会为指定的数组返回一个新的 Illuminate\Support\Collection 实例
//构造函数
public function __construct($items = [])
{
    //可以直接将多种类型转换为数组 Laravel Eloquent ORM 也以集合的形式返回数据
    $this->items = $this->getArrayableItems($items);
}
// 创建一个新的集合
$newCollection = collect([1, 2, 3, 4, 5]);
```

### 静态函数 times()
```PHP
静态 times 方法通过调用给定次数的回调函数来创建新集合：

public static function times($number, callable $callback = null)
{
    if ($number < 1) {
        return new static;
    }
    if (is_null($callback)) {// 回调函数为空，直接返回range()
        return new static(range(1, $number));
    }
    return (new static(range(1, $number)))->map($callback);//给定次数调用回调函数
}
// 基本用法
> Illuminate\Support\Collection::times(10, function ($number) {
    return $number * 9;
})all();
=> [9, 18, 27, 36, 45, 54, 63, 72, 81, 90]

// 回调函数为空，直接返回range()
> Illuminate\Support\Collection::times(2)->all();
=> [1,2,]
```
### 懶集合 LazyCollection
>LazyCollection 类利用了PHP的生成器来在保持低内存使用率的同时使用非常大的数据集 关键字（yield）。
```PHP
use App\LogEntry;
use Illuminate\Support\LazyCollection;

LazyCollection::make(function () {
    $handle = fopen('log.txt', 'r');
    while (($line = fgets($handle)) !== false) {
        yield $line;
    }
})->chunk(4)->map(function ($lines) {
    return LogEntry::fromLines($lines);
})->each(function (LogEntry $logEntry) {
    // Process the log entry...
});
```

### 基本数据处理
#### avg()












