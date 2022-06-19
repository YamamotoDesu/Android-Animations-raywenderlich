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
    <td valign="top"><img width="250" src="https://user-images.githubusercontent.com/47273077/174468287-99850692-2576-41d6-a606-f37380f9e8cd.gif"/></td>
    <td valign="top"><img width="300"  src="https://user-images.githubusercontent.com/47273077/173582564-e0280e77-ee97-4302-af38-4295e4f83010.png"/></td>
  </tr>
</table>

