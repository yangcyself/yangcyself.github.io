# CUE
- what is ORM stands for when relating with SQL and objective languages
- what is PDF language build from? 
# Examples of DSL
## strings
- format strings 
  - > Surprise! A DSL embedded in another language
  - printf, scanf
  - **type safety** and **performace** is studied by compilers
    - `printf('%f,%f',int_number)`
    - `pirntf('%s%s%s',s1,s2,s3)' is faster than `printf(s1+s2+s3)`
  - RegEx
- WEB
  - html
  - templating
- Data
  - **ORM** object relationship mapping
    - mapping object semantics to query
  - Protocol buffer
- AI/ML/DL
  - tf can be regarded as a language, 毕竟变量定义直接是call function
- EDU
  - logo
    - 小学时候电脑课和方旖旎玩的那个小王八
    - 这东西有实体玩具
  - scratch
- DOC
  - post script
    - 一个使用逆波兰表达式书写的画图，渲染，写文档的语言
  - **pdf**， 
    - **Suprise!** pdf is a binary language, stack based language for rendering
  - pandoc things
  - tyntax highlighting files
# Taxonomy of front ends
一个语言算是有自己的前端的，一个语言的理解应该是，前端（语言的表示形式），<---> IR（abstract semantic）, <---> Interpreter or compiler

- strings
- binary files
  - fontfiles, pdf
- XML/JSON/YAML
  - (declarative languages) ? what does this mean?
- **Procedure calls**
  - openGL, GUI tool kitsm OpenCV, MPI
  - > when you write a C-compatible language, always keep a context object to manage memories and other things.
- AST constructors
  - Tensorflow
  - Halide
- Operator overloading
- visual programming

# How to implement (protopying)
1. Define IR(AST)
   - can use Ocaml
   - or use class inherentance to represent AST
2. make a simple interpreter
   1. advice, capture as much information as possible in debug
3. 

