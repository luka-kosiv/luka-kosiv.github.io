---
layout: post
date: 2017-03-04 08:50:28
categories: алгоритмы java
title: 14. Longest Common Prefix
author_name : Luka Kosiv
author_url : /author/lukosiv
author_avatar: lukosiv
show_avatar : true
feature_image: feature-san-fran
show_related_posts: true
square_related: recommend-san-fran
---

> Написать функцию поиска самого длинного префикса в массиве строк.

> Сложная: простая.

## Анализ

Пример: `"abcd", "abcde", "abzz", "abcdef", "abhh".`

Итак, нам нужно найти общий префикс. Префикс --- это начало каждого слова. Если мы возьмем первое слово, 
в нем уже будет искомый префикс, но не ясно где он заканчивается. Потому нам нужно подобрать необходимую длинну. 
Подбирать длину можно несколькими способами:

* принять за префикс первый символ и увиличивать длину;
* принять за префикс все первое слово целиком и уменьшать длину;

Что бы убедиться, что префикс действительно присутствует во всех словах нам необходимо переборать все слова. 
Сложность в таком случае будет `O(n)`, где `n` --- количество слов.

Начнем пребор слов слева на право. Перебирая слова мы будем проверять, начинается ли текущее слово на текущий префикс.
Если мы выбрали способ подбора длины увеличением --- мы будем наращивать длину до тех пор, пока префикс будет входить 
в текущее слово. 

Например, текущий префикс `a`, текущее слово `abcde`. Наращиваем префикс от `a` до `abcd`. 
Идем далее, следующее слово `abzz` не содержит текущий префикс, потому префикс нужно уменьшать до `ab`. 
Таким образом можем дойти до конца массива и получить ответ.

Если мы изначально выбрали другой способ подбора префикса, то мы бы начали с префикса длиной в `abcd` и постепенно, 
**только уменьшали** его, дойдя до `ab`. Этот способо также дает ответ.

Остается открытым вопрос: какой же метод выбрать? 
Если сравнивать производительность на больших строках --- методы работают приблизительно одинаково, 
но реализация второго способа проще:


{% highlight java %}
public class LongestCommonPrefix {

    public static void main(String[] args) {
        System.out.println(longestPrefix(new String[]{
                "abcd", "abcde", "abcdef", "abzz", "abhh"
        }));
    }

    private static String longestPrefix(String[] strings) {
        if (strings == null || strings.length == 0) return "";

        String prefix = strings[0];

        int wordIndex = 1;
        while (wordIndex < strings.length) {
            while (strings[wordIndex].indexOf(prefix) != 0) {
                prefix = prefix.substring(0, prefix.length() - 1);
                System.out.println();
            }
            wordIndex++;
        }
        return prefix;
    }
}

{% endhighlight %}

<!-- ![view]({{site.url}}/{{site.baseurl}}img/post-assets/view.jpg) -->