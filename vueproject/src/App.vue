<template>
  <div class="row">
    <div class="col" v-for="item in commodityList">
      <div class="product type-product">
        <div class="woocommerce-LoopProduct-link">
          <div class="product-image">
            <a href="#" class="wp-post-image">
              <img class="image-cover" :src="item.imageCover" alt="product">
              <img class="image-secondary" :src="item.imageSecondary" alt="product">
            </a>
            <div class="yith-wcwl-add-button show">
              <a href="#" class="add_to_wishlist">
                <i class="zmdi zmdi-favorite-outline"></i>
              </a>
            </div>
            <div class="button add_to_cart_button">
              <a href="#">
                <img src="static/images/icons/shopping-cart-black-icon.png" alt="cart">
              </a>
            </div>
            <h5 class="woocommerce-loop-product__title"><a href="#">{{item.name}}</a></h5>
            <span class="price">
												<del>
													<span class="woocommerce-Price-amount amount">
														<span class="woocommerce-Price-currencySymbol">￥</span>
														{{item.formalPrice}}
													</span>
												</del>
												<ins>
													<span class="woocommerce-Price-amount amount">
														<span class="woocommerce-Price-currencySymbol">￥</span>
														{{item.price}}
													</span>
												</ins>
											</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        commodityList: [

        ]
      };
    },
    mounted: function(){
      this.submitForm('');
    },
    methods: {
      submitForm(formName) {
        this.$axios.defaults.headers.post['Content-Type'] = 'application/json;charset=UTF-8';
        var params = {
          type: "0"
        };
        this.$axios.post(
          '/api/commodity/getCommodityList', //url
          JSON.stringify(params)
        ).then(
          res => {
            this.commodityList = res.data.data;
          },
          error => {
            console.log(error);
            alert('系统出错QAQ');
          }
        )

      }
    }
  }
</script>
<style>
  .form_container {
    -webkit-border-radius: 5px;
    border-radius: 5px;
    -moz-border-radius: 5px;
    background-clip: padding-box;
    margin: 180px auto;
    width: 350px;
    padding: 35px 50px 15px 25px;
    background: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;
  }
</style>
