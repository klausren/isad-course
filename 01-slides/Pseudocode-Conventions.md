# Reading Pseudocode — 伪代码约定（学生用 / Student handout）

> **You do not need to know any programming language for this course.**
> Every code-looking box in the slides is **pseudocode**: structured English that shows
> *what an object knows and what it can do*. You only need to **read** it — never to write it.
> 本课程不要求任何编程基础。课件里所有"代码"都是伪代码，只需要**看得懂**，不需要会写。

---

## 1. The five things you will see（只有 5 种写法）

| What it looks like | What it means | 中文 |
|---|---|---|
| `Class Order` | There is a kind of thing called **Order**. Capital letter = a class. | 一个叫 Order 的类 |
| `− lines : OrderLine[0..*]` | Order **knows** many OrderLines. `−` = private (inside only), `[0..*]` = zero or more. | Order 内部持有若干 OrderLine；`−` 私有，多重性 |
| `+ addItem(item, qty)` | Order **can do** `addItem`. `+` = public (anyone may ask). | Order 对外提供 addItem 操作；`+` 公有 |
| `Class Circle extends Ellipse` | Circle is a **special kind of** Ellipse; it inherits everything Ellipse has. | Circle 是 Ellipse 的子类，继承其全部 |
| `Class CampusCard implements PaymentMethod` | CampusCard **promises** to provide everything PaymentMethod lists. | CampusCard 实现 PaymentMethod 接口 |

Everything else is plain English:

```
    + total() : Money
        sum = ZERO                     # start from zero
        for each line in lines         # repeat for every line
            sum = sum + line.subtotal()
        return sum                     # hand the result back
```

- `#` starts a **comment** — a note for the human reader, not an instruction.
- Indentation (the spaces at the left) shows what belongs inside what.
- `if …`, `for each …`, `return …`, `refuse …` mean what they say in English.
- `→` (or `->`) means "leads to": `if type = CARD → chargeCard(order)`.

## 2. Pseudocode ↔ UML cheat sheet（与类图的对应）

| In a class diagram | In pseudocode |
|---|---|
| Class box `Order` | `Class Order` |
| Attribute `- status : OrderStatus` | `- status : OrderStatus` |
| Operation `+ total() : Money` | `+ total() : Money` |
| `«interface» PaymentMethod` | `PaymentMethod (interface)` |
| Generalization arrow (Circle → Ellipse) | `Class Circle extends Ellipse` |
| Realization arrow (dashed) | `Class CampusCard implements PaymentMethod` |
| Association `Order — OrderLine 0..*` | `- lines : OrderLine[0..*]` |

**This is the whole point**: pseudocode is the class diagram written as lines of text.
If you can read the diagram, you can read the box. 能读类图就能读伪代码。

## 3. Words you can safely ignore（看到可以直接跳过的词）

`public` / `private` / `protected` → in this course we always write them as `+` / `−` / `#`.
Type names after a colon (`: Money`, `: OrderLine[0..*]`) just say **what kind of value** it is —
like units in physics. You never have to memorise them.

## 4. If you want to go further（可选，不为考核要求）

Small code sketches that prove a pattern works are **optional Bonus (C2)**. If you write some,
any language is fine (Python, JavaScript, Java …) and it must be pushed to your repo with a
one-paragraph explanation. Not writing a single line of code costs you **nothing** in this course.

---

*Conventions used across W01–W16 slides. See also: `04-项目实践/Course-Project-Grading-Rubric.md` §3 (Bonus).*
