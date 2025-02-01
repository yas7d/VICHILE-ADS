<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نموذج إعلان مركبة متطور</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #4F46E5;
            --secondary-color: #6366F1;
            --accent-color: #818CF8;
            --background: #f8fafc;
            --text-color: #1e293b;
            --border-color: #e2e8f0;
        }

        body {
            font-family: 'Tajawal', sans-serif;
            background: var(--background);
            margin: 0;
            padding: 15px;
            min-height: 100vh;
            direction: rtl;
            color: var(--text-color);
        }

        .form-container {
            background: white;
            border-radius: 16px;
            padding: 25px;
            width: 100%;
            max-width: 600px;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
            margin: 20px auto;
        }

        .form-step {
            display: none;
            opacity: 0;
            transform: translateX(40px);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .form-step.active {
            display: block;
            opacity: 1;
            transform: translateX(0);
        }

        .step-header {
            text-align: center;
            margin-bottom: 25px;
        }

        .step-header h2 {
            margin: 0;
            font-size: 1.4rem;
            color: var(--text-color);
        }

        .step-progress {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 20px 0;
            position: relative;
        }

        .step-circle {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            background: #f1f5f9;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
            font-size: 0.9rem;
            color: #64748b;
            position: relative;
            z-index: 2;
            transition: all 0.3s ease;
            border: 2px solid transparent;
            cursor: pointer;
        }

        .step-circle.active {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            box-shadow: 0 4px 12px rgba(79, 70, 229, 0.25);
            border-color: var(--primary-color);
        }

        .progress-line {
            position: absolute;
            height: 2px;
            background: #f1f5f9;
            width: 85%;
            left: 7.5%;
            top: 50%;
            transform: translateY(-50%);
        }

        .input-group {
            margin-bottom: 15px;
            position: relative;
        }

        .input-group label {
            display: block;
            margin-bottom: 6px;
            font-weight: 500;
            color: var(--text-color);
            font-size: 0.85rem;
        }

        .input-group input,
        .input-group select,
        .input-group textarea {
            width: 100%;
            padding: 10px 12px;
            border: 1.5px solid var(--border-color);
            border-radius: 8px;
            font-size: 0.9rem;
            transition: all 0.2s ease;
            background: white;
            color: var(--text-color);
        }

        .input-group input:focus,
        .input-group select:focus,
        .input-group textarea:focus {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
            outline: none;
        }

        .icon-options {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .icon-option {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 15px;
            border: 2px solid var(--border-color);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s ease;
            background: white;
            text-align: center;
        }

        .icon-option.active {
            border-color: var(--primary-color);
            background: rgba(79, 70, 229, 0.1);
        }

        .country-option {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px;
            border: 2px solid var(--border-color);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s ease;
            background: white;
        }

        .country-option.active {
            border-color: var(--primary-color);
            background: rgba(79, 70, 229, 0.1);
        }

        .country-flag {
            width: 24px;
            height: 16px;
            border-radius: 4px;
        }

        #uploadContainer {
            border: 2px dashed var(--border-color);
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s ease;
            margin-top: 15px;
        }

        #previewContainer {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 20px;
        }

        .thumbnail {
            width: 100px;
            height: 100px;
            border-radius: 8px;
            overflow: hidden;
            position: relative;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .thumbnail img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .remove-btn {
            position: absolute;
            top: 5px;
            left: 5px;
            background: rgba(255, 0, 0, 0.8);
            color: white;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 12px;
        }

        .form-actions {
            display: flex;
            justify-content: space-between;
            margin-top: 25px;
            gap: 12px;
        }

        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.2s ease;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
        }

        .btn-secondary {
            background: #f1f5f9;
            color: #475569;
        }

        .hidden {
            display: none;
        }

        /* تعديلات على الخطوة الثالثة */
        #step3 .icon-options {
            gap: 8px;
        }

        #step3 .icon-option {
            padding: 10px;
            font-size: 0.8rem;
        }

        #step3 .icon-option i {
            font-size: 1.2rem;
        }

        #step3 .input-group {
            margin-bottom: 10px;
        }

        #step3 .input-group label {
            font-size: 0.9rem;
        }

        #step3 .help-text {
            font-size: 0.75rem;
        }

        .price-group {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }

        .price-group input {
            flex: 1;
        }

        /* تعديلات على الخطوة 8 */
        #step8 .step-progress {
            display: none;
        }
    </style>
</head>
<body>
    <div class="form-container">
        <div class="step-progress">
            <div class="progress-line"></div>
            <div class="step-circle active" onclick="changeStep(1)">1</div>
            <div class="step-circle" onclick="changeStep(2)">2</div>
            <div class="step-circle" onclick="changeStep(3)">3</div>
            <div class="step-circle" onclick="changeStep(4)">4</div>
            <div class="step-circle" onclick="changeStep(5)">5</div>
            <div class="step-circle" onclick="changeStep(6)">6</div>
            <div class="step-circle" onclick="changeStep(7)">7</div>
            <div class="step-circle" onclick="changeStep(8)">8</div>
        </div>

        <!-- الخطوة 1: اختيار الدولة -->
        <div class="form-step active" id="step1">
            <div class="step-header">
                <h2>اختيار الدولة</h2>
            </div>
            
            <div class="input-group">
                <label>الدولة</label>
                <div class="icon-options">
                    <div class="country-option" data-code="+971" onclick="selectCountry('الإمارات', this)">
                        <img src="https://flagcdn.com/ae.svg" class="country-flag" alt="علم الإمارات">
                        <span>الإمارات العربية المتحدة</span>
                    </div>
                    <div class="country-option" data-code="+966" onclick="selectCountry('السعودية', this)">
                        <img src="https://flagcdn.com/sa.svg" class="country-flag" alt="علم السعودية">
                        <span>المملكة العربية السعودية</span>
                    </div>
                    <div class="country-option" data-code="+965" onclick="selectCountry('الكويت', this)">
                        <img src="https://flagcdn.com/kw.svg" class="country-flag" alt="علم الكويت">
                        <span>الكويت</span>
                    </div>
                    <div class="country-option" data-code="+968" onclick="selectCountry('عمان', this)">
                        <img src="https://flagcdn.com/om.svg" class="country-flag" alt="علم عمان">
                        <span>سلطنة عمان</span>
                    </div>
                    <div class="country-option" data-code="+974" onclick="selectCountry('قطر', this)">
                        <img src="https://flagcdn.com/qa.svg" class="country-flag" alt="علم قطر">
                        <span>قطر</span>
                    </div>
                    <div class="country-option" data-code="+973" onclick="selectCountry('البحرين', this)">
                        <img src="https://flagcdn.com/bh.svg" class="country-flag" alt="علم البحرين">
                        <span>البحرين</span>
                    </div>
                    <div class="country-option" data-code="+20" onclick="selectCountry('مصر', this)">
                        <img src="https://flagcdn.com/eg.svg" class="country-flag" alt="علم مصر">
                        <span>مصر</span>
                    </div>
                    <div class="country-option" data-code="+964" onclick="selectCountry('العراق', this)">
                        <img src="https://flagcdn.com/iq.svg" class="country-flag" alt="علم العراق">
                        <span>العراق</span>
                    </div>
                    <div class="country-option" data-code="+962" onclick="selectCountry('الأردن', this)">
                        <img src="https://flagcdn.com/jo.svg" class="country-flag" alt="علم الأردن">
                        <span>الأردن</span>
                    </div>
                </div>
                <small class="help-text">اختر الدولة التي تريد الإعلان فيها</small>
            </div>

            <div class="input-group">
                <label>المنطقة</label>
                <select id="regionSelect" multiple required>
                    <option value="أخرى">أخرى</option>
                </select>
                <small class="help-text">اختر منطقة أو منطقتين (اختياري)</small>
            </div>

            <div class="form-actions">
                <button class="btn btn-primary" onclick="nextStep(2)">التالي</button>
            </div>
        </div>

        <!-- الخطوة 2: نوع المركبة -->
        <div class="form-step" id="step2">
            <div class="step-header">
                <h2>نوع المركبة</h2>
            </div>
            
            <div class="input-group">
                <label>اختر النوع</label>
                <div class="icon-options">
                    <div class="icon-option" data-type="car" onclick="selectVehicleType('car')">
                        <i class="fas fa-car"></i>
                        <span>سيارة</span>
                    </div>
                    <div class="icon-option" data-type="truck" onclick="selectVehicleType('truck')">
                        <i class="fas fa-truck"></i>
                        <span>شاحنة</span>
                    </div>
                    <div class="icon-option" data-type="motorcycle" onclick="selectVehicleType('motorcycle')">
                        <i class="fas fa-motorcycle"></i>
                        <span>دراجة نارية</span>
                    </div>
                </div>
                <small class="help-text">اختر نوع المركبة التي تريد الإعلان عنها</small>
            </div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(1)">السابق</button>
                <button class="btn btn-primary" onclick="nextStep(3)">التالي</button>
            </div>
        </div>

        <!-- الخطوة 3: أسئلة إضافية -->
        <div class="form-step" id="step3">
            <div class="step-header">
                <h2>أسئلة إضافية</h2>
            </div>

            <!-- 1- هل الإعلان بيع أو إيجار؟ -->
            <div class="input-group">
                <label>نوع الإعلان</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectAdType('بيع', this)">
                        <i class="fas fa-hand-holding-usd"></i>
                        <span>بيع</span>
                    </div>
                    <div class="icon-option" onclick="selectAdType('إيجار', this)">
                        <i class="fas fa-file-contract"></i>
                        <span>إيجار</span>
                    </div>
                </div>
            </div>

            <!-- 2- هل المركبة جديدة أو مستعملة؟ -->
            <div class="input-group">
                <label>حالة المركبة</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'vehicleCondition', 'جديدة')">
                        <i class="fas fa-car-side"></i>
                        <span>جديدة</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'vehicleCondition', 'مستعملة')">
                        <i class="fas fa-car-crash"></i>
                        <span>مستعملة</span>
                    </div>
                </div>
            </div>

            <!-- 3- هل تريد نشر مركبة أو قطع غيارها أو اكسسوارات خاصة بها؟ -->
            <div class="input-group" id="adCategoryGroup">
                <label>نوع الإعلان</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'adCategory', 'مركبة')">
                        <i class="fas fa-car"></i>
                        <span>مركبة</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'adCategory', 'قطع غيار')">
                        <i class="fas fa-cogs"></i>
                        <span>قطع غيار</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'adCategory', 'اكسسوارات')">
                        <i class="fas fa-toolbox"></i>
                        <span>اكسسوارات</span>
                    </div>
                </div>
            </div>

            <!-- 4- هل المركبة للتصدير فقط أو للتصدير والاستخدام؟ -->
            <div class="input-group" id="exportGroup">
                <label>نوع العرض</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'exportType', 'تصدير فقط')">
                        <i class="fas fa-globe"></i>
                        <span>تصدير فقط</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'exportType', 'تصدير واستخدام')">
                        <i class="fas fa-globe-americas"></i>
                        <span>تصدير واستخدام</span>
                    </div>
                </div>
            </div>

            <!-- 5- هل المركبة مسجلة داخل الدولة أو لا؟ -->
            <div class="input-group" id="registrationGroup">
                <label>حالة التسجيل</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'registration', 'مسجلة')">
                        <i class="fas fa-check-circle"></i>
                        <span>مسجلة</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'registration', 'غير مسجلة')">
                        <i class="fas fa-times-circle"></i>
                        <span>غير مسجلة</span>
                    </div>
                </div>
            </div>

            <!-- 6- مواصفات المركبة -->
            <div class="input-group">
                <label>مواصفات المركبة</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'specifications', 'خليجية')">
                        <i class="fas fa-flag"></i>
                        <span>خليجية</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'specifications', 'أمريكية')">
                        <i class="fas fa-flag-usa"></i>
                        <span>أمريكية</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'specifications', 'كندية')">
                        <i class="fas fa-flag-canada"></i>
                        <span>كندية</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'specifications', 'أخرى')">
                        <i class="fas fa-ellipsis-h"></i>
                        <span>أخرى</span>
                    </div>
                </div>
            </div>

            <!-- 7- حالة الصبغة -->
            <div class="input-group" id="paintGroup">
                <label>حالة الصبغة</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'paintCondition', 'صبغة الوكالة')">
                        <i class="fas fa-paint-roller"></i>
                        <span>صبغة الوكالة</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'paintCondition', 'مصبوغة')">
                        <i class="fas fa-paint-brush"></i>
                        <span>مصبوغة</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'paintCondition', 'مصبوغة قليلاً')">
                        <i class="fas fa-brush"></i>
                        <span>مصبوغة قليلاً</span>
                    </div>
                </div>
            </div>

            <!-- سعر البيع -->
            <div class="input-group" id="priceGroup">
                <label>السعر المطلوب</label>
                <input type="number" id="price" placeholder="أدخل السعر المطلوب">
            </div>

            <!-- طريقة الدفع -->
            <div class="input-group" id="paymentGroup">
                <label>طريقة الدفع</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="togglePaymentOption(this, 'cash')">
                        <i class="fas fa-money-bill-wave"></i>
                        <span>كاش</span>
                    </div>
                    <div class="icon-option" onclick="togglePaymentOption(this, 'installment')">
                        <i class="fas fa-credit-card"></i>
                        <span>تقسيط</span>
                    </div>
                </div>
            </div>

            <!-- أسعار الإيجار -->
            <div class="input-group" id="rentalPricesGroup">
                <label>أسعار الإيجار</label>
                <div class="price-group">
                    <input type="number" id="dailyPrice" placeholder="السعر اليومي">
                    <input type="number" id="weeklyPrice" placeholder="السعر الأسبوعي">
                </div>
                <div class="price-group">
                    <input type="number" id="monthlyPrice" placeholder="السعر الشهري">
                    <input type="number" id="yearlyPrice" placeholder="السعر السنوي">
                </div>
            </div>

            <!-- سعر التأمين -->
            <div class="input-group" id="insurancePricesGroup">
                <label>سعر التأمين</label>
                <div class="price-group">
                    <input type="number" id="dailyInsurance" placeholder="التأمين اليومي">
                    <input type="number" id="weeklyInsurance" placeholder="التأمين الأسبوعي">
                </div>
                <div class="price-group">
                    <input type="number" id="monthlyInsurance" placeholder="التأمين الشهري">
                    <input type="number" id="yearlyInsurance" placeholder="التأمين السنوي">
                </div>
            </div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(2)">السابق</button>
                <button class="btn btn-primary" onclick="nextStep(4)">التالي</button>
            </div>
        </div>

        <!-- الخطوة 4: التفاصيل الأساسية -->
        <div class="form-step" id="step4">
            <div class="step-header">
                <h2>التفاصيل الأساسية</h2>
            </div>
            
            <div id="dynamicContent">
                <!-- سيتم تعبئة المحتوى هنا حسب نوع المركبة -->
            </div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(3)">السابق</button>
                <button class="btn btn-primary" onclick="nextStep(5)">التالي</button>
            </div>
        </div>

        <!-- الخطوة 5: معلومات الاتصال -->
        <div class="form-step" id="step5">
            <div class="step-header">
                <h2>معلومات الاتصال</h2>
            </div>
            
            <div class="input-group">
                <label>رقم الهاتف</label>
                <div style="display: flex; gap: 10px;">
                    <input type="text" id="countryCode" style="flex: 0 0 80px; background: #f1f5f9;" readonly>
                    <input type="tel" id="phone" style="flex: 1;" required>
                </div>
                <small class="help-text">سيتم استخدام هذا الرقم للتواصل معك</small>
            </div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(4)">السابق</button>
                <button class="btn btn-primary" onclick="nextStep(6)">التالي</button>
            </div>
        </div>

        <!-- الخطوة 6: تحميل الصور -->
        <div class="form-step" id="step6">
            <div class="step-header">
                <h2>تحميل الصور</h2>
            </div>

            <div class="input-group">
                <label>رابط صورة 360 درجة (اختياري)</label>
                <input type="url" id="360image" placeholder="https://example.com/360-image">
            </div>

            <div id="uploadContainer" onclick="document.getElementById('carImages').click()">
                <i class="fas fa-cloud-upload-alt fa-2x"></i>
                <p>انقر لتحميل الصور (حد أقصى 10 صور)</p>
                <input type="file" id="carImages" multiple hidden accept="image/*">
            </div>

            <div id="previewContainer"></div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(5)">السابق</button>
                <button class="btn btn-primary" onclick="nextStep(7)">التالي</button>
            </div>
        </div>

        <!-- الخطوة 7: باقات الإعلان -->
        <div class="form-step" id="step7">
            <div class="step-header">
                <h2>اختيار الباقة</h2>
            </div>

            <div class="icon-options" style="flex-direction: column; gap: 15px;">
                <div class="icon-option" onclick="selectPackage('normal')">
                    <div style="display: flex; justify-content: space-between; width: 100%;">
                        <div>
                            <h3 style="margin: 0;">🆓 إعلان عادي مجاني</h3>
                            <small>مدة العرض: 7 أيام - مشاهدات محدودة</small>
                        </div>
                        <span style="color: var(--primary-color); font-weight: bold;">مجاني</span>
                    </div>
                </div>

                <div class="icon-option" onclick="selectPackage('turbo')">
                    <div style="display: flex; justify-content: space-between; width: 100%;">
                        <div>
                            <h3 style="margin: 0;">🚀 اشتراك توربو المميز</h3>
                            <small>عرض لمدة شهر - مشاهدات 20x - عدد لا محدود من الإعلانات</small>
                        </div>
                        <span style="color: var(--primary-color); font-weight: bold;">259 درهم</span>
                    </div>
                </div>
            </div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(6)">السابق</button>
                <button class="btn btn-primary" onclick="nextStep(8)">متابعة</button>
            </div>
        </div>

        <!-- الخطوة 8: الدفع -->
        <div class="form-step" id="step8">
            <div class="step-header">
                <h2>الدفع الإلكتروني</h2>
            </div>

            <div class="input-group">
                <label>رقم البطاقة</label>
                <input type="text" id="cardNumber" placeholder="1234 5678 9012 3456" maxlength="19">
            </div>

            <div style="display: flex; gap: 15px;">
                <div class="input-group" style="flex: 1;">
                    <label>تاريخ الانتهاء</label>
                    <input type="text" id="expiryDate" placeholder="MM/YY" maxlength="5">
                </div>
                
                <div class="input-group" style="flex: 1;">
                    <label>CVV</label>
                    <input type="text" id="cvv" placeholder="123" maxlength="3">
                </div>
            </div>

            <div class="input-group">
                <label>اسم صاحب البطاقة</label>
                <input type="text" id="cardName" placeholder="الاسم كما هو على البطاقة">
            </div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(7)">السابق</button>
                <button class="btn btn-primary" onclick="submitForm()">اكتمال الدفع</button>
            </div>
        </div>
    </div>

    <script>
        // بيانات المركبات الكاملة
        const vehicleData = {
            car: {
                brands: ["تويوتا", "فورد", "بي إم دبليو", "مرسيدس", "أودي", "نيسان", "هيونداي", "كيا", "شيفروليه", "فولكسفاغن", "رينو", "بيجو", "سوزوكي", "ميتسوبيشي", "هوندا", "جيب", "لكزس", "فولفو", "مازدا", "سكودا"],
                models: ["كورولا", "كامري", "راف4", "لاند كروزر", "هايلكس", "فوكس", "موستانج", "إكسبلورر", "X5", "الفئة الثالثة", "الفئة الخامسة", "الفئة السابعة", "A4", "A6", "Q5", "Q7", "صني", "باترول", "قاشقاي", "جوك", "ألتيما", "اكسنت", "توسان", "سانتافي", "النترا", "سوناتا", "سيراتو", "سبورتاج", "سورينتو", "بيكانتو", "سول", "كروز", "كابتيفا", "تاهو", "سيلفرادو", "ماليبو", "جولف", "تايجر", "باسات", "تيغوان", "أماروك", "داستر", "لوجان", "كوليوس", "كابتور", "ميجان", "208", "301", "3008", "5008", "508", "سويفت", "فيتارا", "جيمني", "بالينو", "سياز", "لانسر", "باجيرو", "ASX", "اوتلاندر", "ميراج", "سيفيك", "أكورد", "CR-V", "سيتي", "بي إل آر", "رينيجيد", "جراند شيروكي", "كومباس", "رانجلر", "جلاديتور", "IS", "ES", "RX", "NX", "LX", "S60", "XC90", "XC60", "V90", "S90", "3", "6", "CX-5", "CX-9", "MX-5", "أوكتافيا", "سوبرب", "كودياك", "فابيا", "كاروك"],
                categories: ["سيدان", "SUV", "كوبيه", "هاتشباك", "بيك أب", "فان"]
            },
            truck: {
                brands: ["فولفو", "مرسيدس", "سكانيا", "مان", "دايملر", "إيفيكو", "بيتربيلت", "كينوورث", "فريتلاينر", "ماك", "هينو", "تاتا", "ماهيندرا"],
                models: ["FH16", "أكتروس", "R系列", "TGS", "Actros", "Arocs", "Antos", "TGX", "TGS", "TGM", "TGL", "Stralis", "Eurocargo", "Daily", "Cascadia", "T680", "W900", "Coronado", "122SD", "Pinnacle", "Granite", "Anthem", "Lonestar", "ProStar", "Dump Truck", "Flatbed", "Tanker", "Refrigerator"],
                categories: ["ثقيلة", "متوسطة", "خفيفة", "نقل بضائع", "نقل حاويات", "نقل سيارات"]
            },
            motorcycle: {
                brands: ["هارلي ديفيدسون", "هوندا", "ياماها", "كاواساكي", "سوزوكي", "دوكاتي", "بي إم دبليو", "تريومف", "ك تي إم", "أبريليا", "إنديان"],
                models: ["سبورتستر", "CBR", "YZF-R1", "Ninja", "GSX-R", "Panigale", "S1000RR", "Street Triple", "Duke", "RSV4", "Scout"],
                categories: ["كلاسيكية", "رياضية", "سكوتر", "طرق وعرة", "تريل"]
            }
        };

        // بيانات الدول ورموزها
        const countryCodes = {
            'الإمارات': '+971',
            'السعودية': '+966',
            'الكويت': '+965',
            'عمان': '+968',
            'قطر': '+974',
            'البحرين': '+973',
            'مصر': '+20',
            'العراق': '+964',
            'الأردن': '+962'
        };

        // بيانات المناطق لكل دولة
        const regions = {
            'الإمارات': ['دبي', 'أبوظبي', 'الشارقة', 'عجمان', 'رأس الخيمة', 'الفجيرة', 'أم القيوين', 'أخرى'],
            'السعودية': ['الرياض', 'جدة', 'مكة', 'المدينة', 'الدمام', 'الخبر', 'أخرى'],
            'الكويت': ['الكويت', 'الفروانية', 'حولي', 'الأحمدي', 'الجهراء', 'مبارك الكبير', 'أخرى'],
            'عمان': ['مسقط', 'صلالة', 'صحار', 'نزوى', 'صور', 'أخرى'],
            'قطر': ['الدوحة', 'الريان', 'الخور', 'الوكرة', 'أخرى'],
            'البحرين': ['المنامة', 'المحرق', 'الرفاع', 'مدينة حمد', 'أخرى'],
            'مصر': ['القاهرة', 'الإسكندرية', 'الجيزة', 'شرم الشيخ', 'الأقصر', 'أسوان', 'أخرى'],
            'العراق': ['بغداد', 'البصرة', 'الموصل', 'أربيل', 'السليمانية', 'أخرى'],
            'الأردن': ['عمان', 'إربد', 'الزرقاء', 'العقبة', 'الكرك', 'أخرى']
        };

        let currentStep = 1;
        let selectedVehicleType = null;
        let selectedCountry = null;
        let selectedPackage = null;
        let adType = null;
        let adCategory = null;
        let paymentOptions = [];

        function selectCountry(country, element) {
            selectedCountry = country;
            document.querySelectorAll('.country-option').forEach(opt => opt.classList.remove('active'));
            element.classList.add('active');
            document.getElementById('countryCode').value = countryCodes[country];

            // تحديث قائمة المناطق بناءً على الدولة المحددة
            const regionSelect = document.getElementById('regionSelect');
            regionSelect.innerHTML = regions[country].map(region => `<option value="${region}">${region}</option>`).join('');
        }

        function selectVehicleType(type) {
            selectedVehicleType = type;
            document.querySelectorAll('.icon-option').forEach(opt => opt.classList.remove('active'));
            document.querySelector(`[data-type="${type}"]`).classList.add('active');
            loadDynamicContent();
        }

        function selectAdType(type, element) {
            adType = type;
            document.querySelectorAll('#step3 .icon-option').forEach(opt => opt.classList.remove('active'));
            element.classList.add('active');
            toggleAdOptions();
        }

        function selectOption(element, group, value) {
            const options = element.parentElement.querySelectorAll('.icon-option');
            options.forEach(opt => opt.classList.remove('active'));
            element.classList.add('active');

            // حفظ القيمة المحددة
            switch (group) {
                case 'vehicleCondition':
                    vehicleCondition = value;
                    break;
                case 'adCategory':
                    adCategory = value;
                    break;
                case 'exportType':
                    exportType = value;
                    break;
                case 'registration':
                    registration = value;
                    break;
                case 'specifications':
                    specifications = value;
                    break;
                case 'paintCondition':
                    paintCondition = value;
                    break;
            }
            toggleAdOptions();
        }

        function toggleAdOptions() {
            const exportGroup = document.getElementById('exportGroup');
            const paintGroup = document.getElementById('paintGroup');
            const registrationGroup = document.getElementById('registrationGroup');
            const priceGroup = document.getElementById('priceGroup');
            const paymentGroup = document.getElementById('paymentGroup');
            const rentalPricesGroup = document.getElementById('rentalPricesGroup');
            const insurancePricesGroup = document.getElementById('insurancePricesGroup');

            if (adType === 'إيجار') {
                paintGroup.style.display = 'none';
                registrationGroup.style.display = 'none';
                priceGroup.style.display = 'none';
                paymentGroup.style.display = 'none';
                rentalPricesGroup.style.display = 'block';
                insurancePricesGroup.style.display = 'block';
            } else {
                paintGroup.style.display = 'block';
                registrationGroup.style.display = 'block';
                priceGroup.style.display = 'block';
                paymentGroup.style.display = 'block';
                rentalPricesGroup.style.display = 'none';
                insurancePricesGroup.style.display = 'none';
            }

            if (adCategory === 'قطع غيار' || adCategory === 'اكسسوارات') {
                paintGroup.style.display = 'none';
            } else {
                paintGroup.style.display = 'block';
            }
        }

        function togglePaymentOption(element, option) {
            element.classList.toggle('active');
            if (paymentOptions.includes(option)) {
                paymentOptions = paymentOptions.filter(opt => opt !== option);
            } else {
                paymentOptions.push(option);
            }
        }

        function loadDynamicContent() {
            const container = document.getElementById('dynamicContent');
            const data = vehicleData[selectedVehicleType];
            container.innerHTML = `
                <div class="input-group">
                    <label>العلامة التجارية</label>
                    <select>${data.brands.map(b => `<option>${b}</option>`).join('')}</select>
                </div>
                <div class="input-group">
                    <label>الموديل</label>
                    <select>${data.models.map(m => `<option>${m}</option>`).join('')}</select>
                </div>
                <div class="input-group">
                    <label>الفئة</label>
                    <select>${data.categories.map(c => `<option>${c}</option>`).join('')}</select>
                </div>
                <div class="input-group">
                    <label>سنة الصنع</label>
                    <select>
                        ${Array.from({length: 50}, (_, i) => `<option>${2023 - i}</option>`).join('')}
                    </select>
                </div>
            `;
        }

        function selectPackage(pkg) {
            selectedPackage = pkg;
            document.querySelectorAll('.icon-option').forEach(opt => opt.classList.remove('active'));
            event.target.closest('.icon-option').classList.add('active');
        }

        function nextStep(step) {
            if (validateStep(currentStep)) {
                changeStep(step);
            }
        }

        function prevStep(step) {
            changeStep(step);
        }

        function changeStep(step) {
            document.querySelectorAll('.form-step').forEach(s => s.classList.remove('active'));
            document.getElementById(`step${step}`).classList.add('active');
            currentStep = step;
            updateProgress();
        }

        function updateProgress() {
            document.querySelectorAll('.step-circle').forEach((circle, index) => {
                circle.classList.toggle('active', index < currentStep);
            });
        }

        function validateStep(step) {
            let isValid = true;
            if (step === 1) {
                if (!selectedCountry) {
                    isValid = false;
                    alert('يرجى اختيار الدولة');
                }
            }
            if (step === 3) {
                if (!adType || !adCategory) {
                    isValid = false;
                    alert('يرجى اختيار جميع الخيارات المطلوبة');
                }
            }
            return isValid;
        }

        document.getElementById('carImages').addEventListener('change', function(e) {
            const preview = document.getElementById('previewContainer');
            preview.innerHTML = '';
            Array.from(e.target.files).forEach(file => {
                const reader = new FileReader();
                reader.onload = (e) => {
                    const div = document.createElement('div');
                    div.className = 'thumbnail';
                    div.innerHTML = `
                        <img src="${e.target.result}">
                        <div class="remove-btn" onclick="this.parentElement.remove()">✕</div>
                    `;
                    preview.appendChild(div);
                }
                reader.readAsDataURL(file);
            });
        });

        function submitForm() {
            if (validateStep(currentStep)) {
                alert('تم إرسال الإعلان بنجاح!');
                document.querySelectorAll('.form-step').forEach(s => s.classList.remove('active'));
                document.getElementById('step1').classList.add('active');
                currentStep = 1;
                updateProgress();
            }
        }
    </script>
</body>
</html>
