## 컬럼 생성
다음 명령 이용
```
rails generate migration add_payment_to_biz_purchases imp_uid:string merchant_uid:string status:string

```
20180321025459_add_payment_to_biz_purchases.rb
```
class AddPaymentToBizPurchases < ActiveRecord::Migration[5.1]
  def change
    add_column :biz_purchases, :imp_uid, :string
    add_column :biz_purchases, :merchant_uid, :string
    add_column :biz_purchases, :status, :string
  end
end
```

bundle exec rake db:migrate
schema.rb 업데이트됨

bundle exec rake db:rollback


# Gemfile.lock
의존성 변경으로 오류나는 경우가 잦기 때문에 이 파일을 보존해야한다.
bundle update를 사용하면 Gemfile.lock이 업데이트 된다.
bundle install 사용
