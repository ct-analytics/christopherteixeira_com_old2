---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "When Machine Learning Fails"
summary: "An overview of the challenges in using machine learning and some suggestions on how to overcome them."
authors: 
  - admin
tags: 
  - Other
categories: 
  - Machine Learning
date: 2021-01-19T20:39:53-05:00
slides:
  # Choose a theme from https://github.com/hakimel/reveal.js#theming
  theme: league
  # Choose a code highlighting style (if highlighting enabled in `params.toml`)
  #   Light style: github. Dark style: dracula (default).
  highlight_style: github
---

# When Machine Learning Fails

## Christopher Teixeira
April 1, 2021

---

## A little about me

### Christopher Teixeira
#### Principal Data Scientist 
#### [The MITRE Corporation](www.mitre.org) 
- MS in Operations Research from George Mason University
- BS in Mathematics from Worcester Polytechnic Institute

---

## Notable inventions 
<div class="flex-parent">
	<div class="input-flex-container">
		<input type="radio" name="timeline-dot" data-description="1">
		<div class="dot-info" data-description="1">
			<span class="year">May 2006</span>
			<span class="label">Graduate with BSc in Mathmatics from WPI</span>
		</div>
		<input type="radio" name="timeline-dot" data-description="2">
		<div class="dot-info" data-description="2">
			<span class="year">June 2006</span>
			<span class="label">Start at SAIC</span>
		</div>
		<input type="radio" name="timeline-dot" data-description="3" checked>
		<div class="dot-info" data-description="3">
			<span class="year">November 2010</span>
			<span class="label">Start at IBM</span>
		</div>
    <input type="radio" name="timeline-dot" data-description="4">
		<div class="dot-info" data-description="4">
			<span class="year">December 2010</span>
			<span class="label">Graduate with MS in Operations Research from GMU</span>
		</div>
		<input type="radio" name="timeline-dot" data-description="5">
		<div class="dot-info" data-description="5">
			<span class="year">August 2012</span>
			<span class="label">Start at Epsilon</span>
		</div>
		<input type="radio" name="timeline-dot" data-description="6">
		<div class="dot-info" data-description="6">
			<span class="year">July 2014</span>
			<span class="label">Start at MITRE</span>
		</div>
		<!--vdiv id="timeline-descriptions-wrapper">
			<p data-description="1">And future Call of Duty players would thank them.</p>
			<p data-description="2">Because every kid should get to be Tarzan for a day.</p>
			<p data-description="3">And the world rejoiced.</p>
			<p data-description="4">Because building roads is inconvenient.</p>
			<p data-description="5">Ain’t nobody got time to rake.</p>
			<p data-description="6">Because paper currency is for noobs.</p>
		</div -->
	</div>
</div>

```CSS
$numDots: 20
$parentWidthBase: 0.8
$parentWidth: $parentWidthBase * 100vw
$parentMaxWidth: 1000px
$dotWidth: 25px
$active: #2C3E50
$inactive: #AEB6BF

html
	height: 100%
body
	min-height: 100%
body
	font-family: 'Quicksand', sans-serif
	font-weight: 500
	color: #424949
	background-color: #ECF0F1
	padding: 0 25px
	display: flex
	flex-direction: column
	position: relative
.flex-parent
	display: flex
	flex-direction: column
	justify-content: center
	align-items: center
	width: 100%
	height: 100%
	min-height: 500px
.input-flex-container
	display: flex
	justify-content: space-around
	align-items: center
	flex-wrap: wrap
	width: $parentWidth
	max-width: $parentMaxWidth
	position: relative
	z-index: 0
	margin-left: calc((#{$parentWidth} - #{$dotWidth}) / #{$numDots}) //make up for offset of .dot-info
input
	width: $dotWidth
	height: $dotWidth
	background-color: $active
	position: relative
	border-radius: 50%
	display: block
	-moz-appearance: none
	-webkit-appearance: none
	appearance: none
	cursor: pointer
	&:focus
		outline: none
	&::before, &::after
		content: ''
		display: block
		position: absolute
		z-index: -1
		top: 50%
		transform: translateY(-50%)
		background-color: $active
		width: $parentWidth / $numDots
		height: 5px
		max-width: $parentMaxWidth / $numDots
	&::before
		left: calc(#{-$parentWidth / $numDots} + #{$dotWidth / 2})
	&::after
		right: calc(#{-$parentWidth / $numDots} + #{$dotWidth / 2})
	&:checked
		background-color: $active
		&::before
			background-color: $active
		&::after
			background-color: $inactive
	&:checked
		~ input
			&, &::before, &::after
				background-color: $inactive
		+ .dot-info
			span
				font-size: 13px
				font-weight: bold	

.dot-info
	width: $dotWidth
	height: $dotWidth
	display: block
	// background-color: red
	visibility: hidden
	position: relative
	z-index: -1
	//position each span on top of the dot immediately before it; -1px at the end is just fudging the numbers for rounding error
	left: calc((((#{$parentWidth} - #{$dotWidth}) / #{$numDots}) * -1) - 1px)
	span
		visibility: visible
		position: absolute
		font-size: 12px
		&.year
			bottom: -30px
			left: 50%
			transform: translateX(-50%)
		&.label
			top: -65px
			left: 0
			transform: rotateZ(-45deg)
			width: 70px
			text-indent: -10px

#timeline-descriptions-wrapper
	width: 100%
	margin-top: 140px
	font-size: 22px
	font-weight: 400
	margin-left: calc((-#{$parentWidth} - #{$dotWidth}) / #{$numDots}) //make up for offset of .dot-info
	p
		margin-top: 0
		display: none


// magic shenanigans
$descriptions: '1910', '1920', '1930', '1940', '1950', '1960', '1970', '1980', '1990', '2000'

@each $desc in $descriptions
	input[data-description="#{$desc}"]:checked ~ #timeline-descriptions-wrapper
		p[data-description="#{$desc}"]
			display: block




@media (min-width: $parentMaxWidth / $parentWidthBase)
	.input-flex-container
		margin-left: #{($parentMaxWidth / $numDots) + ($dotWidth / 2)}
	input
		&::before
			left: #{-($parentMaxWidth / $numDots) + ($dotWidth / 2)}
		&::after
			right: #{-($parentMaxWidth / $numDots) + ($dotWidth / 2)}
	.dot-info
		left: calc((((#{$parentMaxWidth} - #{$dotWidth}) / #{$numDots}) * -1) - 1px)
	#timeline-descriptions-wrapper
		margin-left: #{-($parentMaxWidth / $numDots) + ($dotWidth / 2)}
	

@media (max-width: 630px)
	.flex-parent
		justify-content: initial
	.input-flex-container
		flex-wrap: wrap
		justify-content: center
		width: 400px
		height: auto
		margin-top: 15vh
		margin-left: 0
		padding-bottom: 30px
	input, .dot-info
		width: 60px
		height: 60px
		margin: 0 10px 50px
	input
		background-color: transparent !important
		z-index: 1
		&::before, &::after
			content: none
		&:checked
			+ .dot-info
				background-color: $active
				span
					&.year
						font-size: 14px
					&.label
						font-size: 12px
	.dot-info
		visibility: visible
		border-radius: 50%
		z-index: 0 // position behind input, so input remains clickable
		left: 0
		margin-left: -70px
		background-color: $inactive
		span
			&.year
				top: 0
				left: 0
				transform: none
				width: 100%
				height: 100%
				display: flex
				justify-content: center
				align-items: center
				color: #ECF0F1
			&.label
				top: calc(100% + 5px)
				left: 50%
				transform: translateX(-50%)
				text-indent: 0
				text-align: center
	#timeline-descriptions-wrapper
		margin-top: 30px
		margin-left: 0
		text-align: center

@media (max-width: 480px)
	.input-flex-container
		width: 340px

@media (max-width: 400px)
	.input-flex-container
		width: 300px
```

---

## Tell me a little about you

Insert a poll on academic background

---

## What is Machine Learning?

---

## What can it be used for?

---

## Machine Learning can be great
- Helps you 

---

## Sometimes things go wrong...
- highlight a couple news stories

---

## What are some causes for these issues?

---

## How can you avoid these?

---

## Thank you

Christopher Teixeira <br>
[cteixeira@mitre.org](mailto:cteixeira@mitre.org)

<i class="fab fa-linkedin"></i> [linkedin.com/in/christopherteixeira](https://www.linkedin.com/in/christopherteixeira/)
<i class="fab fa-twitter-square"></i> [@CT_Analytics](https://twitter.com/CT_Analytics)