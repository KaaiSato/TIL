# 変数型
```java
int sample1;
sample1 = 4;

long sample2;
sample2 = 10000000000000;

var sample3 = 10;  //　型推論
```


## ArrayList（可変長配列：要素数を変更できる）
```java
import java.util.ArrayList;  //ライブラリをインポート

class Main {
  public static void main(String[] args) {
    ArrayList<Integer> scores = new ArrayList<Integer>(); //配列のデータ型を指定してscoresとして宣言

    scores.add(1); //要素の追加、addメソッド
    scores.add(5);
    scores.add(10);
    scores.add(15);

    System.out.println(scores.get(0)); //要素の出力
    System.out.println(scores.get(1));
    System.out.println(scores.get(2));
    System.out.println(scores.get(3));
  }
}
```