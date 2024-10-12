# Daily Record
## Day1 10/3
### 1. 观看了9月30号课程的回放，学会了git的基本使用。
```
git add .  //将更改添加到暂存区
git commit -m "modify structs"  //提交暂存区的更改
git push origin main  //推送到远程仓库
```
### 2. 完成了structs,enums,strings和modules的练习题。学会了struct的初始化以及如何用更新模板一部分值，保持其余的不变。熟悉了&str和String的一些操作，如字符串拼接，去除两端空白字符以及替换指定字符串。
```Rust
let your_order = Order{name: String::from("Hacker in Rust"), count: 1, ..order_template}; // 除了name和count，其余的值全部和order_template一致。

input.trim(); // 去除两端空白字符串，返回&str，不会改变input，返回一个新变量
input.replace("cars", "balloons"); //将cars替换为balloons，返回的是String类型，不会改变input
```
## Day2 10/4
### 完成了hashmap练习题,在对hashmap进行修改时，不能同时取出一个以上的mut变量修改。
```Rust
let mut& basket: HashMap<Fruit, u32>;
baskey.entry(fruit).or_insert(100); //如果不存在fruit，则插入并赋值为100
```
## Day3 10/5
### 完成了options,error_handling,generics,quiz2,traits练习题。
```Rust
//在match语句中使用条件语句进行判断
match time_of_day {
    x if x < 22 => Some(5),
    x if x < 24 => Some(0),
    _ => None,
}

//将Option转为Result类型使用map_or，into函数对于实现了Into特征的类都可以进行类型转换
assert_eq!(
    generate_nametag_text("Beyoncé".into()).map_or(Err("`name` was empty; it must be nonempty."), |v| Ok(v)),
    Ok("Hi! My name is Beyoncé".into())
);

//?可以提取Option和Result中Some()和Ok()中的值，如果是None或Err则会返回None或Err
let qty = item_quantity.parse::<i32>()?;

//Vec的pop方法返回的是Option类型
while let Some(Some(integer)) = optional_integers.pop() {
    assert_eq!(integer,cursor);
    cursor -= 1;
}

//Box<dyn Trait> 可以动态分配，实现多态
```
## Day4 10/6
### 完成了iterators,lifetimes,smart_pointers,tests,quiz3练习题。
```Rust
/*
三种类型的迭代器：
1、iter,只能读数据
2、iter_mut,对数据进行引用，可以修改数据
3、into_iter,拥有数据的所有权

collect方法可以将迭代器收集在一起
map方法遍历迭代器，将迭代器中的数据传进闭包进行修改
fold方法可以遍历迭代器，设置一个初始值，将迭代器中的元素累积在一个元素中

生命周期用来确保引用不会在无效内存区域进行

四种类型的指针：
1、Box
2、Rc，引用计数指针，只能有一个mut引用，可以有多个引用
3、Arc，适用于多线程的引用计数指针
4、Cow，可以拥有数据的所有权，也可以借用数据

#[should_panic],在测试时如果panic则测试通过
*/
//问题1，iterators文件中的iterator3.rs
fn result_with_list() -> Result<Vec<i32>, DivisionError> {
    let numbers = vec![27, 297, 38502, 81];
    //为什么unwrap能够通过而?不行
    let division_results = numbers.into_iter().map(|n| divide(n, 27).unwrap()).collect();//正确
    //let division_results = numbers.into_iter().map(|n| divide(n, 27)?).collect();//错误
    //let division_results = numbers.into_iter().map(|n| divide(n, 27)).collect::<Result<Vec<i32>, DivisionError>>(); 正确
    Ok(division_results0)
}
```
## Day5 10/7
### 完成了clippy,conversions,macros,tests,threads练习题
```Rust
//问题2，conversions文件中的as_ref_mut.rs
fn num_sq<T: AsMut<u32>>(arg: &mut T) {
    // TODO: Implement the function body.
    //为什么不能是*arg
    let num = *arg.as_mut(); //正确
    //let num = *arg;错误
    *arg.as_mut() = num * num;
}
//问题3，tests文件中的test5
unsafe fn modify_by_address(address: usize) {
    // TODO: Fill your safety notice of the code block below to match your
    // code's behavior and the contract of this function. You may use the
    // comment of the test below as your format reference.
    unsafe {
        // todo!("Your code goes here")
        let a_mut = address as *mut u32; //正确
        //let a_mut = address as *mut usize; 错误
        //为什么改成u32就对了，usize不对
        *a_mut = 0xAABBCCDD;
    }
}
//问题4，tests文件中的test6.rs
unsafe fn raw_pointer_to_box(ptr: *mut Foo) -> Box<Foo> {
    // SAFETY: The `ptr` contains an owned box of `Foo` by contract. We
    // simply reconstruct the box from that pointer.
    let mut ret: Box<Foo> = unsafe {
        Box::from_raw(ptr)
    };
    unsafe {
        ret.b = Some("hello".to_string())
        //*ret.b = Some("hello".to_string()) 错误
        //自动解引用是如何实现的
    };
    ret
}
```
## Day6 10/8
### 
## Day7 10/9
###
## Day9 10/10
### 完成了algorithm练习题，第一阶段编程题全部完成。
## Day10 10/11
### 配置好了rCore-Camp的实验环境。
## Day11 10/12
```shell
//用于检查文件类型的命令
file target/riscv64gc-unknown-none-elf/debug/os
//反汇编代码，执行反汇编时报错，发现没有rust-objdump命令，找了半小时，发现需要安装cargo-binutils和添加llvm-tools-preview组件。
rust-objdump -S target/riscv64gc-unknown-none-elf/debug/os
```
