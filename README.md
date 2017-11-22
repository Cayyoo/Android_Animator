# Android_Animator
属性动画Animator

```java
/**
 * 属性动画Animator：
 *  Android动画TimeInterpolator（插值器）和TypeEvaluator（估值器）
 */

/**
 * 总结——常用属性
 *
 * ObjectAnimator可以调用各种属性，只要这个属性具有get/set方法，我们就可以操纵它，
 * 如果这个属性没有提供get/set方法，或者我们想自定义一个属性，来让它进行一些改变，
 * 那么我们就要定义一个Property（属性），去实现它的set/get方法，就可以操作这样一个属性。
 *
 * ObjectAnimator常用的一些操作属性：
 * 1. translationX\translationY
 * 2. rotation、rotationX\rotationY，这里的rotation是指3D的旋转。rotationX是水平方向的旋转，rotationY是垂直方向的旋转。
 * 3. scaleX\scaleY  水平、垂直方向的缩放。
 * 4. X\Y  具体会移动到的某个点。
 * 5. alpha  透明度
 * 属性动画框架执行的效率更高、效果更好。
 */

/**
 * 总结——常用方法、类
 * 1. ValueAnimator 数值发生器，可以实现很多很灵活的动画效果
 * 2. ObjectAnimator 是ValueAnimator的一个子类，它封装了ValueAnimator，让我们更轻松地使用属性动画框架。
 *    我们通过ObjectAnimator来操作一个对象的属性，让对象产生一个动画效果。
 * 3. AnimatorUpdateListener 监听事件
 * 4. AnimatorListenerAdapter 监听事件
 * 5. PropertyValuesHolder 控制动画集合的显示效果、顺序和流程控制
 * 6. AnimatorSet 控制动画集合的显示效果、顺序和流程控制
 * 7. TypeEvaluators  估值计算器
 * 8. Interpolators  插值器
 * 估值计算器和插值器用来控制具体产生的数值的一个变化规律以及变化状态。
 */

/**
 * 除了ValueAnimator.ofInt()，还有其他类型的数字生成器，其中ValueAnimator.ofObject()可以实现自定义的数字生成器。
 * 参数中的fraction就是时间因子（0到1之间变化的数值）。通过fraction、startValue、endValue，通过各种各样的计算方式，
 * 就可以生成所有想要产生的值，不光能产生普通数据结构，通过泛型还可以定义更为复杂的数据结构。
 *   ValueAnimator animator = ValueAnimator.ofObject(new TypeEvaluator() {
 *      @Override
 *      public Object evaluate(float fraction, Object startValue, Object endValue) {
 *         return null;
 *      }
 *   });
 *
 *   生成泛型PointF（float类型的点坐标）：
 *   ValueAnimator animator = ValueAnimator.ofObject(new TypeEvaluator<PointF>() {
 *      @Override
 *      public PointF evaluate(float fraction, PointF startValue, PointF endValue) {
 *         return null;
 *      }
 *   });
 *   在方法evaluate()中可以添加各种各样的计算方式。
 */

/**
 * ValueAnimator：
 * 1. 之前学过ObjectAnimator是作用于某一控件的某一属性，而ValueAnimator本身不作用于任何属性，本身也不会提供任何动画，
 *    简单而言，ValueAnimator是一个数值发生器，可以产生任何你想要的数值，Android系统给它提供了很多数值计算方法。
 * 2. 那么，产生这些数值有什么用呢？其实，在属性动画中，如何产生每一步的具体动画效果，都是通过 ValueAnimator 计算出来的。
 *    比如要实现一个0到100的位移动画，随着时间的持续，数值也从0到100递增，有这些值，就可以作用这些属性，让它产生动画效果。
 * 3. 那么，ValueAnimator 是如何产生这些值的呢？
 *    首先，ValueAnimator 会根据动画已经进行的时间和总时间的比值，产生一个0到1的时间因子，有了这样的时间因子，
 *       经过相应的变换，就可以根据你的StartValue和EndValue，来生成中间的相应的值。同时，通过插值器的使用，
 *       我们还可以进一步控制每一个时间因子的产生值的变化速度，比如我们使用线性插值器，生成数值的时候就是一个线性变化，
 *       只要时间相同，增量就相同。
 *    由于 ValueAnimator 本身不响应任何一个动画，也不能控制任何一个属性，所以它并没有 ObjectAnimator 使用得那么广泛。
 * 4. 查看源码，我们可以发现 ObjectAnimator 是继承了 ValueAnimator。之前也说过了，
 *    正是由于 ValueAnimator 产生的动画变化的变化值，ObjectAnimator 才可以将它应用于我们的属性。
 *    因此，ObjectAnimator 实际上是对ValueAnimator的封装。
 * 5. 那么，如何通过 ValueAnimator 去实现动画效果呢？这就需要使用动画监听事件了，
 *    我们可以监听ValueAnimator每一步所产生的值，通过这个值去实现相应的动画效果。
 *    如0-100的计时器
 */
```

![](https://github.com/ykmeory/Android_Animator/blob/master/img/linear.png "线性动画")
![](https://github.com/ykmeory/Android_Animator/blob/master/img/sector.png "扇形动画")
</br>
![](https://github.com/ykmeory/Android_Animator/blob/master/img/1_ObjectAnimator.png "")

![](https://github.com/ykmeory/Android_Animator/blob/master/img/1_ValueAnimator.png "")

![](https://github.com/ykmeory/Android_Animator/blob/master/img/2_ValueAnimator.png "")

![](https://github.com/ykmeory/Android_Animator/blob/master/img/3_Attributes.png "常用属性")

![](https://github.com/ykmeory/Android_Animator/blob/master/img/4_method.png "常用方法")

![](https://github.com/ykmeory/Android_Animator/blob/master/img/5_Interpolator.png "插值器")
