```c++
list.cbegin() // return a const iterator
std::find_if

  auto it = std::find_if(handlers_.cbegin(), handlers_.cend(),
                         [&prefix](const UrlHandler& entry) { return prefix == entry.prefix_; }); // lambda
             
             
             
             
```


匿名函数
https://blog.csdn.net/xiaoguyin_/article/details/79798362


```c++
int c = 1;

    auto test = [&c](double a, double b) -> int {
        return (int) (a + b + c);
    };

    cout<< test(1.1, 2) << endl;
```


find_if   终止条件, 是否等于iterator的end


string_view 



string find
```c++
std::string::size_type query_index = path_and_query.find('?');
if (query_index == std::string::npos) {
  query_index = path_and_query.size();
}
```


std::move