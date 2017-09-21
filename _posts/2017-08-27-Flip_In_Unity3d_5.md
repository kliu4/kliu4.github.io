---
title: "Flip Character in Unity3d 5"
categories:
  - Unity3d
tags:
  - Unity3d
  - C#
---

{% include toc title="Flip Character in Unity3d 5" icon="file-text" %}

## Introduction

In Unity3d 5, there is built-in "Flip" support. You don't need to write your own facingRight

## Soution

```liquid
public class Player : MonoBehaviour {
	private Rigidbody2D myRigidbody2D;
	private SpriteRenderer sprite;
  
  private void Flip(){
		if (!Mathf.Approximately (myRigidbody2D.velocity.x, 0f))
			sprite.flipX = myRigidbody2D.velocity.x < 0f;
	}
}
```
