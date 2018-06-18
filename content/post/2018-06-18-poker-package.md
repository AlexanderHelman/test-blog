---
title: Poker Package
author: ~
date: '2018-06-18'
slug: poker-package
categories: []
tags: []
---

Last week for my iXperience class, I made an R package for poker-related functions. The first function I wrote generated a random 5-card hand. The second took a 5-card hand as input and returned what hand it was (i.e., one pair, two pair, etc.). Going forward, I would like to extend this project to support functionality for generating any number of 2-card Texas Hold'em starting hands, as well as generate flops, rivers, and turns (all while without repeating cards). Moreover, I'd like to make it so that my package can take two or more Hold'em hands as input and return the probability that each hand comes out on top by the river.