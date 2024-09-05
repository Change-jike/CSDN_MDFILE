> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/129745542?spm=1001.2014.3001.5502)

### 时间字符串格式化，时间字符串不符合规范，转为一般[时间格式](https://so.csdn.net/so/search?q=%E6%97%B6%E9%97%B4%E6%A0%BC%E5%BC%8F&spm=1001.2101.3001.7020)；

PATTERNS ： 预处理的非标准化时间格式，  
STANDARD_PATTERN ： 理想的标准时间格式；

```
/**
     * 时间格式缺少空格
     * 例：2018-11-3013:28:09
     * @param dateStr 需要格式化的 date 字符串
     * @return 标准格式 String 类型的 date;
     */
    public static String dateStringFormat(String dateStr) {
        final String UNKNOWN_TIME = "未知";
        final String[] PATTERNS = {"yyyy-MM-ddHH:mm", "yyyy-MM-dd HH:mm", "yyyy-MM-ddHH:mm:ss"};
        final String STANDARD_PATTERN = "yyyy-MM-dd HH:mm:ss";
        if (StringUtils.isNotBlank(dateStr) && !UNKNOWN_TIME.equals(dateStr)) {
            for (String pattern : PATTERNS) {
                if (isValidDateFormat(dateStr, pattern)) {
                    return DateUtils.dateToStr(DateUtils.parseStrToDate(dateStr, pattern), STANDARD_PATTERN);
                }
            }
        }
        return dateStr;
    }

/**
     * 检查给定的日期字符串是否符合指定的日期格式
     * 例：2018-11-3013:28:09
     * @param dateString 	日期字符串
     * @param pattern 		日期格式字符串
     */
    public static boolean isValidDateFormat(String dateString, String pattern) {
    /*
		SimpleDateFormat 类来解析日期字符串，并设置 setLenient(false) 属性以禁用宽容模式，
		这意味着它只会接受严格匹配指定日期格式的字符串.
		*/
        SimpleDateFormat sdf = new SimpleDateFormat(pattern);
        sdf.setLenient(false);
        
		/*
		它尝试将日期字符串解析为 Date 对象，并检查解析后的日期是否与原始日期字符串完全匹配。
		如果匹配，则返回 true，否则返回 false。
		如果解析过程中发生异常，则捕获 ParseException 并返回 false。
		*/
        try {
            Date date = sdf.parse(dateString);
            if (!dateString.equals(sdf.format(date))) {
                throw new ParseException("Invalid date format", 0);
            }
            return true;
        } catch (ParseException ex) {
            return false;
        }
    }

```