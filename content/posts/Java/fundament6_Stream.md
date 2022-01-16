---
title: "Java Fundament 6: Stream"
date: 2021-10-06T18:18:55+08:00
draft: true
toc: false
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Fundament
---



```java
public class StreamTestCase1 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("a");
        list.add("aa");
        list.add("aaa");
        list.add("asbcdef");
        Stream<Integer> stream = list.stream().map(String::length);
        stream.forEach(System.out::println);

        boolean anyMatch = list.stream().anyMatch(element -> element.contains("a"));
        System.out.println(anyMatch);

        Stream<String> streamFilter = list.stream().filter(element -> element.contains("a"));
        streamFilter.forEach(System.out::println);

        Integer[] ints = {5, 1, 2, 3};
        List<Integer> list1 = Arrays.asList(ints);

        Optional<Integer> plus = list1.stream().reduce((a,b) -> a * b);
        Optional<Integer> sum = list1.stream().reduce(Integer::sum);
        System.out.println(plus.orElse(0));
        System.out.println(sum.orElse(0));
    }
}
```

