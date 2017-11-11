### 获取最近更新的时间;
 getUpdateTime(date) {
    if (date == null) {
      return null;
    }
    let diff = new Date().getTime() - new Date(date).getTime();
    console.log(diff);
    let minute = 60 * 1000; // 1分钟
    let hour = 60 * minute; // 1小时
    let day = 24 * hour; // 1天
    let month = 31 * day; // 月
    let year = 12 * month; // 年
    let r = 0;
    if (diff > year) {
      r = diff / year;
      return Math.round(r) + "年前";
    }
    if (diff > month) {
      r = diff / month;
      return Math.round(r) + "个月前";
    }
    if (diff > day) {
      r = diff / day;
      return Math.round(r) + "天前";
    }
    if (diff > hour) {
      r = diff / hour;
      return Math.round(r) + "小时前";
    }
    if (diff > minute) {
      r = diff / minute;
      return Math.round(r) + "分钟前";
    }
    return "刚刚";
  }`