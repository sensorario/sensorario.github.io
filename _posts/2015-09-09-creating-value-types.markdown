---
layout: post
title:  "Creating Value Types"
date:   2015-09-09
tags: tdd, value types
---

<article>Objects have a state. Objects have an identity. Objects have reltionship with other objects. Values types are immutable, and this means that they have no meaningful identity.</article>
<article>Specific types, reduce the risk of confusion. Anytime we have a type that define a concept, it guide us towards using a more object-oriented approach instead of scattering related behavior across the code.</article>
<article>
    Basically I know three moments that push me to introduce a new value type:
    <ul>
        <li>When an object code become yoo complex</li>
        <li>When new concept domain comes in the code</li>
        <li>When more values are always used together</li>
    </ul>
</article>
<article>
    <h2>Breaking out</h2>
    <p>When the code in an object become too complex, maybe it is
    implementing too many concepts. To improve the design, we can break
    out coherent units of behavior into helper types.</p>
</article>
<article>
    <h2>Buddling off</h2>
    <p>If we need to introduce a new whole concept of the domain, maybe its
    the time to introduce a new value type. Its possible that the new object
    has no attributes. Dont worry: when the code grows, fields and method
    will be added inside the new value type.</p>
</article>
<article>
    <h2>Bundling up</h2>
    <p>When we have two or more object, always used together, maybe we can
    introduce the missing concept. We can now hide their fields behind a
    clean interface, satisfying the "composite simpler that the sum of its
    parts" principle.</p>
</article>
