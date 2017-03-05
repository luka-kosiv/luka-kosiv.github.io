---
layout: post
date: 2017-03-04 08:50:28
categories: coding js
author_name : Luka Kosiv
author_url : /author/lukosiv
author_avatar: lukosiv
show_avatar : true
feature_image: street-foster-city
show_related_posts: true
square_related: recommend-laptop
---

Написать функцию поиска самого длинного префикса в массиве строк.

Ключевой момент в том, что префикс это начало каждого слова.
Потому для начала предпологаем что все первое слово и есть искомый префикс.
Если это не так - уменьшаем первеое слово в длинне (убираем последний символ), до тех пор пока не найдем общюю часть.

{% highlight java %}
public class LongestCommonPrefix {

  public static void main(String[] args) {
    System.out.println(longestCommonPrefix(new String[]{
      "abcde", "abcd", "abcdef", "abzz","abhh"
    }));
  }

  private static String longestCommonPrefix(String[] stringsArray) {
    if (stringsArray == null || stringsArray.length == 0) return "";

      String prefix = stringsArray[0];

      int wordIndex = 1;
      
      while (wordIndex < stringsArray.length) {
        while (stringsArray[wordIndex].indexOf(prefix) != 0) {
          prefix = prefix.substring(0, prefix.length() - 1);
            System.out.println();
        }
        wordIndex++;
      }
      return prefix;
  }
}

{% endhighlight %}