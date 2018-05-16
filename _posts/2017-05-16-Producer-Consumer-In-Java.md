---
title: "Producer and Consumer using Java Multi-Threading"
categories:
  - Java
tags:
  - Java
  - Multi-Threading
---

{% include toc title="Producer and Consumer using Java Multi-Threading" icon="file-text" %}

## Introduction

A simple model using java multi-threading for producer and consumer problem.

## Code
```liquid
class Producer implements Runnable {
    Clerk clerk;

    public Producer(Clerk clerk) {
        this.clerk = clerk;
    }

    @Override
    public void run() {
        System.out.println("Start to produce products");
        while (true) {
            try {
                Thread.sleep((int)(Math.random()* 1000));
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            clerk.produceProduct();
        }
    }
}

class Consumer implements Runnable {
    Clerk clerk;

    public Consumer(Clerk clerk) {
        this.clerk = clerk;
    }

    @Override
    public void run() {
        System.out.println("Start to consume products");
        while (true) {
            try {
                Thread.sleep((int)(Math.random()* 1000));
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            clerk.consumeProduct();
        }
    }
}

class Clerk{
    int product = 0;

    public synchronized void consumeProduct() {
        if (product <= 0) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        } else {
            System.out.println(Thread.currentThread().getName() + ": consume product " + product);
            product--;
            notifyAll();
        }
    }

    public synchronized void produceProduct() {
        if (product >= 20) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        } else {
            product++;
            System.out.println(Thread.currentThread().getName() + ": produce product " + product);
            notifyAll();
        }
    }
}

public class TestProduct {
    public static void main(String[] args) {
        Clerk clerk = new Clerk();
        Producer producer1 = new Producer(clerk);
        Producer producer2 = new Producer(clerk);
        Consumer consumer1 = new Consumer(clerk);
        Thread thread1 = new Thread(producer1);
        Thread thread2 = new Thread(producer2);
        Thread thread3 = new Thread(consumer1);
        thread1.start();
        thread2.start();
        thread3.start();
    }
}
```
