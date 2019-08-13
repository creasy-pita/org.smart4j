1 架构探险 从零开始写 java web 框架的内容  源码


 GClib 动态代理
    代理的创建
        Enhancer.create(targetClass,  MethodInterceptor  interceptor)
    代理与 targetclass 如何联系
        MethodInterceptor 的 intercept方法 会在代理类 调用某方法时被调用 同事传入参数 Object targetObject, Method targetMethod, Object[] methodParams, MethodProxy methodProxy
        intercept方法 内部 通过传入的参数调用指定的目标类方法
    代理的切入点的范围
        切入controller的所有方法
    代理切入范围的优化
        优化内容：
            定义切面（此处切面就是代理类）的方法 切入哪些目标类及以哪种增强类型（比如 before,end,throw,arround)切入
        实现：
            可以在切面类A中 加注解  @pointcut,@before 等，
            代理链执行到A时，根据A的注解判断当前调用的方法是否切人
        举例
            logacepct before,after 不切入 controllerA ,throw 切人 controllerA
            那么targetclass controllerA中的代理链有 logacepct ，但执行logacepct before时会判断切人点的注解没有切人controllerA的方法，所以会略过before log代码
