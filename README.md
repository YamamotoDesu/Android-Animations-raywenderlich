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

