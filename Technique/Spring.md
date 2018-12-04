## [@Resource vs @Autowired](https://stackoverflow.com/questions/4093504/resource-vs-autowired)

* @Resource allows you to specify a name of the injected bean
* @Resource means get me a known resource by name. The name is extracted from the name of the annotated setter or field, or it is taken from the name-Parameter.

* @Autowired allows you to mark it as non-mandatory.
* @Inject or @Autowired try to wire in a suitable other component by type.