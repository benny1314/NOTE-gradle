## Gradle 中使用自定义属性时的 `""` 和  `''`

```
ext{
    springVersion = "4.2.4"    
}

"$springVersion"  # 结果是 4.2.4

'$springVersion'  # 结果是 $springVersion

```