author: Kazuki Otomo
summary: WorkSheet3-1
id: WorkSheet3-1
categories: codelab,markdown
environments: Web
status: Published
feedback link: https://github.com/KazukiOtomo

# ソフトウェアデザイン第3回



## 値オブジェクト

```java
int quantity;
BigDecimal amount;
```

このコードは、数量（quantity）をマイナス21億からプラス21億まで、
金額（amount）をほぼ無限大かつ小数点21億桁まで扱うような宣言になっています。

しかし、業務内で扱う数量や金額はそのような値が登場することはない。
文法的には問題ないが、異常な値が混入する（バグ）可能性が高くなります。

この問題を防ぐために用いるデザインパターンが、**値オブジェクト**です。

Lombokというライブラリを使うと値オブジェクトを簡潔に書くことができます。

Amount.java **（Lombokを使用した版）**
```java
import lombok.Value;

@Value
public class Amount {
    long value;
}
```

実際に生成されているコードは以下のようになります。
注目してほしい点は、

    ・デフォルトコンストラクタ（引数なしコンストラクタ）が生成できない
    ・Setterが利用できない
    ・Getterは利用できる
    ・継承が利用できない

Amount.java **（同じことをやろうとした版）**
```java
public class Amount {
    private final long value;
    private final String name;

    public Amount(final long id, final String name) {
        this.value = id;
        this.name = name;
    }

    public long getValue() {
        return this.value;
    }

    public String getName() {
        return this.name;
    }

    @Override
    public boolean equals(final Object o) {
        if (o == this) return true;
        if (!(o instanceof Amount)) return false;
        final Amount other = (Amount) o;
        if (this.getValue() != other.getValue()) return false;
        final Object this$name = this.getName();
        final Object other$name = other.getName();
        if (this$name == null ? other$name != null : !this$name.equals(other$name)) return false;
        return true;
    }

    @Override
    public int hashCode() {
        final int PRIME = 59;
        int result = 1;
        final long $id = this.getValue();
        result = result * PRIME + (int) ($id >>> 32 ^ $id);
        final Object $name = this.getName();
        result = result * PRIME + ($name == null ? 43 : $name.hashCode());
        return result;
    }

    @Override
    public String toString() {
        return "Amount(id=" + this.getValue() + ", name=" + this.getName() + ")";
    }
}
```



値オブジェクトを活用したクラスの例と用意できるテストを以下に示す。

Merchandice.java
```java
public class Merchandise {

    private final Amount amount;

    public Merchandise(Amount amount) {
        if (amount.getValue() < 0) throw new IllegalArgumentException("負の値が入っています");
        this.amount = amount;
    }
}
```

Merchandise.java
```java
import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.assertThrows;

class MerchandiseTest {

    @Test
    void 金額がマイナスの商品はインスタンス化することができない() {
        assertThrows(IllegalArgumentException.class,
                () -> new Merchandise(new Amount(-1)));
    }
}
```

このテストでは、商品（Merchandise）クラスが異常な値を持つことが絶対にないという検証になっている
と共に、「金額がマイナスになることはない」という**業務におけるルール**も読み取ることができる。



## 演習1

以下のクラス図と指示を読み取った上で実装してください。





## ファーストクラスコレクションパターン

コレクションオブジェクト（List, Set, Map, 配列など）を扱うコードは複雑になりがちです。

例えば、

    ・Listに要素を追加する
    ・Listの0番目を抽出する

といった**副作用**のある処理を複数箇所にわたって書いてしまった場合、
バグの原因となると共に、変更する際のチェック範囲を増加させ、
変更容易性の低いコードとなってしまいます。

*コレクションの参照をそのまま渡したGetterメソッド（よくない例）*
```java
public class Cards {
    private final List<Card> cards;

    // このメソッドを呼び出した先で判断/加工/計算が行われる可能性がある
    public List<Card> getList() {
        return this.cards;
    }
}
```

この問題を解決するためのデザインパターンが、
**ファーストクラスコレクション**パターンです。

これは、コレクション型のインスタンス変数を１つだけ持つ専用クラスを作り、
コレクションに関するロジックをカプセル化することで、
コレクションを操作するロジックをコレクションオブジェクトに閉じ込めることを目指しています。

*サンプルコード（ファーストクラスコレクション）*
```Java
public class Cards {
    private final List<Card> cards;

    // 外部からインスタンス化もできないようにする
    private Cards(){
        this.cards = new ArrayList<Card>();
    }

    // コレクションを操作するロジックをクラス内に閉じ込める
    void add(Card card) { ... }
    void removeIfExist(Card card) { ... }

    int count() { ... }
}
```

また、コレクションオブジェクトは、業務の関心事そのものであることが多いです。

例えば、同じCardインスタンスを持つコレクションオブジェクトでも、
「デッキ」と「手札」では、ルールや振る舞いは異なるものであるはずです。

なので、それぞれ専用のクラスを作り、それぞれに対応した専用のクラスを用意することで
業務ロジックをわかりやすく整理し、コードの変更を楽で安全にすることにつながります。



## 演習2

以下で示すコードには、複数の問題があります。

コードに含まれている問題点を指摘した上で、
改善したクラスを作成してください。（改善箇所や方法は１つとは限りません）

SampleService.java
```java
public class SampleService {

    public void createCustomerList(Customer customer){
        var customers = new Customers();
        var customerList = customers.getCustomerList();
        customerList.add(customer);
    }
}
```

Customer.java
```java
public class Customer {

    final int credit;

    public Customer(int credit) {
        this.credit = credit;
    }
}
```

Customers.java
```java
public class Customers {

    private final List<Customer> customerList;

    public Customers() {
        this.customerList = new ArrayList<>();
    }

    public List<Customer> getCustomerList() {
        return customerList;
    }
}
```

