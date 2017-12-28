---
layout: post
title: Yii — bypassing beforeSave()
---

If you have defined in your model some "actions" / "mutators" in your, `beforeSave` method there is a simple way to prevent that these actions to take place in certain cases when you need that.

For example, having a `Company` model and a field, `unpaid_invoices_count` that you are updating during each saving. If you want that in a certain case, this field not to be updated, instead of saving the model you can use the method `setAttributes($array)` . Here <http://www.yiiframework.com/doc/api/1.1/CModel#setAttributes-detail> you may find details on it.
