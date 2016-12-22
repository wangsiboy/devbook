spring mobile

web.xml

&lt;filter&gt;

&lt;filter-name&gt;deviceResolverRequestFilter&lt;\/filter-name&gt;

&lt;filter-class&gt;org.springframework.mobile.device.DeviceResolverRequestFilter&lt;\/filter-class&gt;

&lt;\/filter&gt;

&lt;filter-mapping&gt;

&lt;filter-name&gt;deviceResolverRequestFilter&lt;\/filter-name&gt;

&lt;url-pattern&gt;\/\*&lt;\/url-pattern&gt;

&lt;\/filter-mapping&gt;

&lt;!-- &lt;mvc:interceptors&gt;

&lt;bean class="org.springframework.mobile.device.DeviceResolverHandlerInterceptor" \/&gt;

&lt;bean class="org.springframework.mobile.device.site.SitePreferenceHandlerInterceptor" \/&gt;

&lt;\/mvc:interceptors&gt;

&lt;mvc:annotation-driven&gt;

&lt;mvc:argument-resolvers&gt;

&lt;bean class="org.springframework.mobile.device.DeviceWebArgumentResolver" \/&gt;

&lt;bean class="org.springframework.mobile.device.site.SitePreferenceWebArgumentResolver" \/&gt;

&lt;\/mvc:argument-resolvers&gt;

&lt;\/mvc:annotation-driven&gt;

&lt;mvc:interceptors&gt;

&lt;bean class="org.springframework.mobile.device.DeviceResolverHandlerInterceptor" \/&gt;

&lt;bean class="org.springframework.mobile.device.switcher.SiteSwitcherHandlerInterceptor" factory-method="mDot"&gt;

&lt;constructor-arg value="localhost:8082" \/&gt;

&lt;\/bean&gt;

&lt;\/mvc:interceptors&gt; 

--&gt;

