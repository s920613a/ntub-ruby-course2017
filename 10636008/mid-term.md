## 說明

1. 答案直接寫在這個 `mid-term.md` 裡，並使用 Markdown 語法撰寫。
1. 題目總共分 Ruby、Rails 以及 Git 三大主題，請在每個主題完成時進行 Commit。
1. 完成後，請發送 PR 至 `mid-term` 分支。
1. 也就是說，你的 PR 應該只會有三或四次的 Commit。

## Ruby 題目 (50 分)

1. (10 分) 請完成本題實作內容

```ruby
class Cat
  def initialize(name)
      @name = name
  end
  def name
      @name
  end
end

kitty = Cat.new("kitty")
puts kitty.name  # 在畫面上印出 kitty 字樣
```

2. (5 分) 假設有個 Hash：

```ruby
profile = {name: "kk", age: 18}
```

當執行這行程式：

```ruby
p profile["name"]
```

會得到什麼結果? 為什麼?

nil,因為在這個Hash中,他的Key是:name(Symbol)而不是"name"(字串),所以會拿不到東西

3. (5 分) 如果要在 1 到 100 的數字當中，任意取出 5 個不重複的亂數，你會怎麼做？
  ```ruby
   puts [*1..100].sample(5)
   ```
4. (10 分)
```ruby
class Bank
  def transfer(amount)
    # ...
  end
end

Bank.transfer(10)
```

上面這段程式碼執行後會發生什麼事？為什麼？如果有錯誤又該如何修正？

mid.rb:7:in `<main>': undefined method `transfer' for Bank:Class (NoMethodError)
要先有了 Bank 類別之後，才可以用這個類別的 new 方法來產生實體，而要透過 new 方法傳參數進來，在類別裡面必須有個名為 initialize 的方法來接收傳進來的參數。在 initialize 方法裡，常見的手法是會把參數傳進來給內部的實體變數（instance variable）
```ruby
class Bank
  def initialize(amount)
    @amount=amount
  end
  def transfer#(amount)
    # ...
  end
end
money = Bank.new(10)
money.transfer
```

5. (10 分) 請問以下方法：

```ruby
link_to "刪除", products_path(product), method: :delete, class: "btn btn-default"
```

`link_to` 方法共有幾個參數？為什麼？

3 個,
```ruby
link_to ("刪除", products_path(product), {method: :delete, class: "btn btn-default"})
```
因為小括號跟大括號(hash的)被省略了

6. (10 分) 在 Ruby 裡面常會看到冒號的寫法，例如：

有的冒號靠右邊：

```ruby
class Store
  has_many :products
end
```

有的冒號靠左邊：

```ruby
link_to "檢視", books_path(book), class: "btn btn-default"
```

或是兩邊都有：

```ruby
user_profile = {name: "kk", age: 18, blood_type: :b_negative}
```

請問，這三種寫法分別代表什麼意思呢？

左邊:Symbol,表示某個狀態,是個帶有名子的物件

右邊:設定的意思,如將age設定成18

兩邊:namespace,為了讓可能同名的方法或類別可以區分，所以在include時要連名帶姓的叫


## Rails 題目 (30 分)

1. (10 分) 請簡述 `bundle install` 指令的用途。

執行時，會去尋找Gemfile裡的套件，並安裝套件

2. (10 分) 請說明 `rails db:migrate` 這個指令的用途是什麼？

會把在db/migrate裡的檔案內的描述轉換成真實的資料

3. (10 分) 假設某個 Controller 的程式碼如下：

```ruby
class BooksController < ApplicationController
  def index
    @books = Book.all
  end

  def update
    @book = Book.find_by(id: params[:id])
    @book.update(price: 100)
    redirect_to books_path, notice: "資料更新成功"
  end
end
```

請問：
- 第 3 行的 `@books` 前面的那個 `@` 是什麼意思？如果把 `@` 拿掉會發生什麼事？
- 第 7 行以及第 8 行的 `@book`，如果把 `@` 拿掉會發生什麼事？為什麼？

實體變數，在MVC架構裡我們不會直接讓view去存取，而會請controller先取得，並變成實體變數，再讓view來取用，因此當拿掉@時，會變成區域變數，會讓view存取不到該變數，進而讓整個網頁看不到出現紅字
如果只拿掉7.8行，那網頁還可以正常開啟，只是當執行update動作時，一樣會找不到變數，因為該變數已變成區域變數
## Git 題目 (20 分)

1. (10 分) 在你想像中的分支(branch)，是個什麼樣子的東西?

branch像是在貼標籤一樣，在節點上貼上標簽來表示
例如o----o----o----o----o

	                                                        abc	     Head

2. (5 分) 空的資料夾無法被加入 Git 版控，但如果就是想讓這個資料夾留下來，你會怎麼處理?

新增一個.gitkeep的檔案，然後再執行add跟commit

3. (5 分) 如果有些檔案，像是 `/config/database.yml` 之類比較機密的檔案，不想放在 Git 裡面，你會怎麼做？

新增一個.gitignore檔案，並編輯加入/config/database.yml

## 額外加分題 (20 分)

在你之前的作業中曾寫到：

```ruby
def odd_number_calculator(n)
  [*1..n].select {|i| i.odd?}.reduce(:+)
end

puts odd_number_calculator(100)  # 得到 2500
```

上述程式中，第 2 行的 `reduce` 後面接了 `:+` 的意思是什麼呢?

reduce像是把數字從左到右(該案例中是從1-100中的偶數)疊起來，而是疊加還是疊減(有這種說法嗎XD)還是疊乘等等，而reduce(:+)括號內的冒號後面就是控制他疊起來時，加減乘除的運算元是哪個
