---
title: "DOW-loop: Notions and Usages"
date: 2025-12-19
draft: false
---

## The structure of DOW-loop

```SAS
DATA ...;
	<stuff done before the loop>;
	DO <index specs> UNTIL (break-event);
		SET A;
		<stuff done for each record>;
    END;
    <stuff done after the loop ...>;
RUN;
```

A DOW-loop separates the data step into three isolated parts. It is the most natural way to enforce different instructions before, in and after the loop. In most situation where DOW-loop is applicable, the input dataset is grouped or sorted, and the break-event is `last.group_var`. In such a case, the DOW-loop divides actions to three steps:

1. between the top of the implied loop (of data step) and before the first observation in a `by group` is read, that is, do some preparation before go through observations in a group;
2. for each observation in the `by group`;
3. after the last record in the `by group`  and before the bottom of the implied loop. It is often used to generate some summary variable (it's like `count, mean, sum` and so on).

