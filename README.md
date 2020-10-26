# kotlin-strategy-pattern

```java
interface FormatterStrategy {
    fun format(value: Double, currency: String): String
}

class TwoDecimalsFormatterStrategy : FormatterStrategy {
    override fun format(value: Double, currency: String): String {
        return String.format("%.2f %s", value, currency)
    }
}

class FourDecimalFormatterStrategy : FormatterStrategy {
    override fun format(value: Double, currency: String): String {
        return String.format("%.4f %s", value, currency)
    }
}

abstract class Money(val value: Double, val currency: String) {
    protected lateinit var formatterStrategy: FormatterStrategy
    fun format() = formatterStrategy.format(value, currency)
}

class Balance(value: Double, currency: String) : Money(value, currency) {
    init {
        formatterStrategy = TwoDecimalsFormatterStrategy()
    }
}

class Fund(value: Double, currency: String) : Money(value, currency) {
    init {
        formatterStrategy = FourDecimalFormatterStrategy()
    }
}
```
