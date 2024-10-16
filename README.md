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
## Day12 10/13
```Rust
/*
Rust宏模式匹配类型有
1. literal 匹配字面量，如字符串、字符、数字或布尔值
2. ident 匹配标识符（identifier），如变量名或函数名。
3. path 匹配路径（通常是模块路径），如 std::io::Read。
4. expr 匹配任意合法的表达式（expression）。
5. ty 匹配类型（type）。
6. stmt 匹配语句（statement）。
7. block 匹配代码块（block），如 { ... }。
8. tt 匹配任意标记树，是最灵活的匹配类型。
9. meta 匹配属性的元信息（metadata），如 #[derive(Debug)]。
10. item 匹配任意 Rust 项目（item），如函数、结构体、枚举等定义。
11. vis 匹配可见性修饰符（visibility），如 pub。
12. lifetime 匹配生命周期参数（lifetime），如 'a。
*/
```
## Day13 10/14
```Rust
OUTPUT_ARCH(riscv) //指定目标架构为 RISC-V。
ENTRY(_start) //定义程序的入口点为 _start。
BASE_ADDRESS = 0x80200000; 
. = BASE_ADDRESS; //.表示当前地址（即程序加载位置）。

la sp, boot_stack_top //la：这是 load address 指令，用于加载符号地址到寄存器中。
```
## Day14 10/15
```Rust
//#[link_section = ".text.entry"]：将entry_point函数放置在.text.entry段中。
#![no_std] // 不链接标准库，适用于嵌入式或低层次开发
#![no_main] // 禁用标准入口点

#[link_section = ".text.entry"] // 将函数放入自定义段
#[no_mangle] // 禁止名字重整，保持函数名不变
pub extern "C" fn entry_point() -> ! {
    // 无限循环，避免函数返回
    loop {}
}

core::arch::global_asm!(include_str!("link_app.S"));
//使用 include_str! 宏将一个外部的汇编文件 link_app.S 的内容读入为字符串，并插入到 Rust 代码中。

macro LOAD_GP n
   ld x\n, \n*8(sp)
endm
//ld x\n, \n*8(sp) 是一条加载指令，从栈指针 sp 指向的地址加载数据到指定的寄存器
```
## Day15 10/16
| **编号** | **别名** | **用途**                            | **说明**                         |
|-----------|----------|-------------------------------------|----------------------------------|
| x0        | `zero`   | 常数 0                              | 读总是返回0，写入无效            |
| x1        | `ra`     | 返回地址寄存器                      | 存储函数调用返回地址             |
| x2        | `sp`     | 栈指针                              | 指向当前栈顶                     |
| x3        | `gp`     | 全局指针                            | 指向全局数据区域                 |
| x4        | `tp`     | 线程指针                            | 指向线程局部存储（TLS）          |
| x5–x7     | `t0–t2`  | 临时寄存器                          | 不需要在函数调用之间保存         |
| x8        | `s0/fp`  | 保存寄存器/帧指针                   | 可用于栈帧基地址                  |
| x9        | `s1`     | 保存寄存器                          | 保存跨函数调用的数据             |
| x10–x11   | `a0–a1`  | 参数/返回值寄存器                  | 用于传递函数参数和返回值         |
| x12–x17   | `a2–a7`  | 参数寄存器                          | 用于传递函数参数                 |
| x18–x27   | `s2–s11` | 保存寄存器                          | 保存跨函数调用的数据             |
| x28–x31   | `t3–t6`  | 临时寄存器                          | 不需要在函数调用之间保存         |

---
