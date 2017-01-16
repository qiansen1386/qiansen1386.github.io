+++
categories = ["dev", "English"]
date = "2016-08-29T17:54:45+08:00"
tags = ["DDD", "OOP"]
title = "DTO, Entity, Value Object, POJO/POCO/POPO 的区别"

+++

DTO vs Entity vs Value Object vs POJO/POCO/POPO
------

Definations:

DTO => Data Transfer Object, a object which contains no logics, used to pass through application bounderies.

Entity => Value Object + identity.(We will not talk about Entity in following articles, you get the idea, they are the same)

Value Object => Value Object can contains methods

POJO/POCO/POPO => Plain Object with/without State(Data properties) + Behavior(methods), both ValueObject & DTO can be considered as POJO.

ref: http://enterprisecraftsmanship.com/2015/04/13/dto-vs-value-object-vs-poco/