# Android Animations: Materials

This repo contains all the downloadable materials and projects associated with the **[Android Animations](https://www.raywenderlich.com/18770099-android-animations)** from [raywenderlich.com](https://www.raywenderlich.com).

Each edition has its own branch, named `versions/[VERSION]`. The default branch for this repo is for the most recent edition.

## Release History

| Branch                                                                                | Version | Release Date |
| ------------------------------------------------------------------------------------- |:-------:|:------------:|
| [versions/2.0](https://github.com/raywenderlich/video-aa-materials/tree/versions/2.0) | 2.0     | 2020-12-08   |
| [versions/1.0](https://github.com/raywenderlich/video-aa-materials/tree/versions/1.0) | 1.0     | 2018-03-26   |

## View Property Animations 

<img width="406" alt="スクリーンショット 2022-06-19 14 38 24" src="https://user-images.githubusercontent.com/47273077/174467449-9ff17542-d52e-4a00-9b59-d9f4c5612e18.gif">

```kt
  private fun setupUi() {
    binding.loginButton.setOnClickListener {
      loginViewModel.logIn()
      animateLogin()
    }
  }

  private fun animateLogin() {
    binding.progressBar.alpha = 0f
    binding.progressBar.visibility = View.VISIBLE

    val alphaAnimator = ValueAnimator.ofFloat(0f,1f)
    alphaAnimator.duration = 1000

    alphaAnimator.addUpdateListener {
      val animationAlpha = it.animatedValue as Float

      binding.progressBar.alpha = animationAlpha
      binding.loginButton.alpha = 1 - animationAlpha
    }

```
<img width="406" src="https://user-images.githubusercontent.com/47273077/174467932-8dbb258f-6c0e-41d9-af64-f31f58e97973.gif">

```kt
  private fun animateLogin() {
    binding.progressBar.alpha = 0f
    binding.progressBar.visibility = View.VISIBLE

    var buttonWight = binding.loginButton.width
    var buttonHeight = binding.loginButton.height

    val alphaAnimator = ValueAnimator.ofFloat(0f,1f)
    alphaAnimator.duration = 1000

    alphaAnimator.addUpdateListener {
      val animatedValue = it.animatedValue as Float

      binding.progressBar.alpha = animatedValue
      binding.loginButton.alpha = 1 - animatedValue * 1.5f

      binding.loginButton.updateLayoutParams {
        this.height = (buttonHeight * (1f - animatedValue)).toInt()
        this.width = (buttonWight * (1f - animatedValue)).toInt()
      }
    }

    alphaAnimator.start()
  }
```

<table>
   <tr>
    <td class="DecelerateInterpolator">DecelerateInterpolator</td>
    <td class="AccelerateInterpolator">AccelerateInterpolator</td>
    <td class="BounceInterpolator">BounceInterpolator</td>
  </tr>
  <tr>
    <td valign="top" class="DecelerateInterpolator"><img width="300" src="https://user-images.githubusercontent.com/47273077/174468287-99850692-2576-41d6-a606-f37380f9e8cd.gif"/></td>
    <td valign="top"  class="AccelerateInterpolator"><img width="300"  src="https://user-images.githubusercontent.com/47273077/174468542-af431336-e072-4ce6-8710-139f7dad472e.gif"/></td>
   <td valign="top"  class="BounceInterpolator"><img width="300"  src="https://user-images.githubusercontent.com/47273077/174468729-e8f95b23-44b7-4803-9251-66430ba9a08f.gif"/></td>
  </tr>
</table>

```kt
    alphaAnimator.interpolator = DecelerateInterpolator()
    alphaAnimator.interpolator = AccelerateInterpolator()
    alphaAnimator.interpolator = BounceInterpolator()
    
```

## Object Property Animations
```kt
    val progressBarAlphaAnimator = ObjectAnimator.ofFloat(binding.progressBar,"alpha", 0f, 1f)
    progressBarAlphaAnimator.duration = 3000
    progressBarAlphaAnimator.interpolator = BounceInterpolator()
    
    progressBarAlphaAnimator.start()
```


## Custom Animation
<img width="406" src="https://user-images.githubusercontent.com/47273077/174476011-2266ec7c-9e3d-4e8e-bd10-da3f74764e02.gif">

```kt
  @RequiresApi(Build.VERSION_CODES.N)
  fun transformToProgress() {
    val drawable = binding.actionButton.background as? GradientDrawable
    val targetWidth = targetButtonWidth
    val targetCornerRadius = targetButtonWidth

    val cornerAnimator = ValueAnimator.ofFloat(drawable?.cornerRadius ?: 0f, targetCornerRadius.toFloat())
    val widthAnimator = ValueAnimator.ofInt(binding.actionButton.measuredWidth, targetWidth)
    val progressBarAlphaAnimator = ObjectAnimator.ofFloat(binding.progressBar, "alpha",0f,1f)

    cornerAnimator.duration = 1000
    widthAnimator.duration = 1000
    progressBarAlphaAnimator.duration = 1000

    cornerAnimator.addUpdateListener {
      drawable?.cornerRadius = it.animatedValue as Float
      binding.actionButton.background = drawable
    }

    widthAnimator.addUpdateListener {
      binding.actionButton.updateLayoutParams {
        this.width = it.animatedValue as Int
      }

      binding.actionButton.textSize = 1f - it.animatedFraction
    }

    binding.progressBar.alpha = 0f
    binding.progressBar.visibility = View.VISIBLE

    widthAnimator.start()
    cornerAnimator.start()
    progressBarAlphaAnimator.start()
  }
```


