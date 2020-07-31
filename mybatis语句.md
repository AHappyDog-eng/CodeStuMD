

```
<select id="queryByOrderId" resultType="Order">
    <!--根据id查询Order并携带OrderDetail实体 -->
    <!--如果告诉mybatis，把结果映射到Order的同时，也要映射到OrderDetail属性-->
    select
    a.orderId,
    a.buyerName,
    a.buyerPhone,
    a.buyerAddress,
    a.orderAmount,
    b.detailId "orderDetail.detailId",
    b.orderId "orderDetail.orderId",
    b.productPrice "orderDetail.productPrice",
    b.productQuantity "orderDetail.productQuantity"
    from Order a
    inner join OrderDetail b on a.orderId = b.orderId
    where a.orderId = #{orderId}
</select>

```

```
<resultMap id="Base_app_post" type="<路径省略>.AppPost">
    <result column="post_id" property="postId"/>
    <result column="post_title" property="postTitle"/>
    <result column="up_time" property="upTime"/>
    <result column="post_type" property="postType"/>
    <result column="points_num" property="pointsNum"/>
    <result column="collection_num" property="collectionNum"/>
    <result column="reply_num" property="replyNum"/>
    <result column="transfer_num" property="transferNum"/>
    <result column="is_host" property="isHost"/>
    <result column="content_type" property="contentType"/>


    <association property="user" javaType="<路径省略>.AppUserMini" resultMap="Base_app_user" />
  </resultMap>

  <resultMap id="Base_app_user" type="<路径省略>.AppUserMini" >
    <result column="user_id" property="userId"/>
    <result column="user_name" property="userName"/>
    <result column="user_sex" property="userSex"/>
    <result column="user_age" property="userAge"/>
    <result column="user_img" property="userImg"/>
    <result column="user_address" property="userAddress"/>
  </resultMap>

  <select id="selectAppByPostId" resultMap="Base_app_post" parameterType="java.lang.String" >
    select a.post_id,a.post_title,a.up_time,a.post_type,a.points_num,a.collection_num,a.reply_num,a.transfer_num,a.is_hot,a.content_type/// 分割线///,b.user_id,b.user_name,b.user_sex,b.user_age,b.user_img,b.user_address
    from service_post a,sys_user b
    where a.post_id = #{postId,jdbcType=INTEGER} AND a.user_id=b.user_id
  </select>
```

