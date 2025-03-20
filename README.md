<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نموذج إعلان مركبة</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://js.stripe.com/v3/"></script>
    <style>
        /* CSS هنا */
        
/* تنسيق الفاتورة */
#invoice {
    background: var(--background);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
.invoice-item {
    display: flex;
    justify-content: space-between;
    padding: 10px 0;
    border-bottom: 1px solid var(--border-color);
}

.invoice-item:last-child {
    border-bottom: none;
}

.invoice-item.total {
    font-weight: bold;
    color: var(--primary-color);
}

.invoice-item.saved {
    color: #28a745; /* لون أخضر */
    font-weight: bold;
}
        .hidden {
    display: none;
}

/* تنسيق حقل إدخال الكود */
#discountCode {
    font-size: 0.9rem;
    transition: all 0.3s ease;
}

#discountCode:focus {
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
    outline: none;
}

/* تنسيق زر تطبيق الخصم */
.btn-secondary {
    background: var(--secondary-color);
    color: white;
    padding: 10px 15px;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s ease;
}

.btn-secondary:hover {
    background: var(--primary-color);
}

/* رسالة الخطأ أو النجاح */
#discountMessage {
    color: var(--primary-color);
    font-weight: 500;
}

#discountMessage.error {
    color: #dc3545;
}

.price-table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
}

.price-table th, .price-table td {
    padding: 10px;
    text-align: center;
    border: 1px solid var(--border-color);
}

.price-table th {
    background-color: var(--primary-color);
    color: white;
    font-weight: bold;
}

.price-table td {
    background-color: var(--background);
}

.price-table input {
    width: 80%;
    padding: 8px;
    border: 1px solid var(--border-color);
    border-radius: 8px;
    font-size: 0.9rem;
    text-align: center;
}



.placeholder i {
    font-size: 24px;
    margin-bottom: 10px;
    color: var(--primary-color);
}

#mainImageBox img.hidden {
    display: none;
}
        
        
        .main-image-indicator {
    border: 3px solid var(--primary-color);
    box-shadow: 0 4px 12px rgba(79, 70, 229, 0.25);
}
        
        
.remove-main-btn {
    position: absolute;
    top: 5px;
    right: 5px;
    background: rgba(255, 0, 0, 0.8);
    color: white;
    width: 24px;
    height: 24px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    font-size: 12px;
    transition: background 0.3s ease;
}

.remove-main-btn:hover {
    background: rgba(255, 0, 0, 1); /* تغيير لون الزر عند التمرير */
}
        
        
        #mainImageBox img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

#mainImageBox img:hover {
    transform: scale(1.05); /* تكبير الصورة قليلاً عند التمرير */
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2); /* ظل عند التمرير */
}
.change-main-btn {
    position: absolute;
    bottom: 10px;
    left: 50%;
    transform: translateX(-50%);
    background: var(--primary-color);
    color: white;
    padding: 8px 16px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 0.9rem;
    transition: background 0.3s ease;
}


.change-main-btn:hover {
    background: var(--secondary-color); /* تغيير لون الزر عند التمرير */
}
        
        
        /* تنسيق مربع الصورة الرئيسية */
#mainImageBox {
    position: fixed;
    top: 10px; /* تقليل المسافة من الأعلى */
    right: 10px; /* تقليل المسافة من اليمين */
    width: 100px; /* تقليل العرض */
    height: 100px; /* تقليل الارتفاع */
    border: 2px solid transparent; /* تقليل سمك الحدود */
    border-radius: 12px; /* تقليل زوايا التدوير */
    background: linear-gradient(135deg, #4F46E5, #818CF8) border-box;
    box-shadow: 0 4px 12px rgba(79, 70, 229, 0.25), 0 0 0 2px rgba(255, 255, 255, 0.5);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    z-index: 1000;
}
#mainImageBox.hidden {
    display: none;
}

#mainImageBox img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 12px; /* زوايا مدورة للصورة */
    transition: transform 0.3s ease, box-shadow 0.3s ease; /* تأثيرات عند التمرير */
}

.main-image-label {
    position: absolute;
    bottom: -25px;
    font-size: 0.9rem;
    color: var(--text-color);
    font-weight: 500;
    background: rgba(255, 255, 255, 0.9); /* خلفية شبه شفافة */
    padding: 5px 10px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
        
        
 /* تنسيق الألوان في صف أفقي */
.color-options.horizontal {
    display: flex;
    flex-wrap: nowrap;
    overflow-x: auto;
    gap: 10px;
    padding: 25px 0;
}

.color-option {
    width: 60px; /* زيادة العرض لاستيعاب النص */
    height: 60px; /* زيادة الارتفاع لاستيعاب النص */
    border-radius: 50%;
    border: 2px solid var(--border-color);
    cursor: pointer;
    transition: all 0.2s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.8rem; /* حجم الخط مناسب */
    color: white;
    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5); /* ظل للنص */
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); /* ظل بسيط للدائرة */
    flex-shrink: 0; /* لمنع الضغط عند التمرير */
    position: relative; /* لإضافة تأثيرات إضافية */
}

.color-option.active {
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
}

.color-option span {
    position: absolute;
    bottom: -20px; /* وضع النص أسفل الدائرة */
    text-align: center;
    width: 100%;
    color: var(--text-color); /* لون النص */
    font-weight: 500; /* سماكة النص */
    white-space: nowrap; /* منع النص من الانتقال لسطر جديد */
}

.color-option:hover span {
    display: block; /* إظهار النص عند التمرير */
}

.color-option:hover {
    transform: scale(1.05); /* تكبير بسيط عند التمرير */
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); /* ظل أكثر عند التمرير */
}

        .color-preview {
    display: flex;
    gap: 10px;
    align-items: center;
}

.color-circle {
    width: 25px;
    height: 25px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 2px solid #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.color-circle span {
    font-size: 0.7em;
    color: #fff;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}
        .review-container {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-top: 20px;
}
.review-card {
    animation: slideIn 0.6s ease forwards;
}

@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateY(30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
.review-card {
    background: white;
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.review-card h3 {
    margin: 0 0 15px 0;
    font-size: 1.2rem;
    color: var(--primary-color);
}

.review-content {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
}

.review-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid var(--border-color);
}

.review-label {
    font-weight: 600;
    color: var(--text-color);
}

.review-value {
    color: #666;
}

.review-images {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
}

.review-images img {
    width: 100px;
    height: 100px;
    object-fit: cover;
    border-radius: 8px;
    border: 2px solid var(--border-color);
    transition: transform 0.2s ease;
}

.review-images img:hover {
    transform: scale(1.1);
    border-color: var(--primary-color);
}
.review-images img {
    cursor: zoom-in;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.review-images img.enlarged {
    transform: scale(2);
    z-index: 1000;
    box-shadow: 0 12px 24px rgba(0,0,0,0.2);
    cursor: zoom-out;
}
        .input-group select,
.input-group input {
    width: 100%;
    padding: 10px 12px;
    border: 1.5px solid var(--border-color);
    border-radius: 8px;
    font-size: 0.9rem;
    transition: all 0.2s ease;
    background: white;
    color: var(--text-color);
}

.input-group select:focus,
.input-group input:focus {
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
    outline: none;
}

.mileage-input {
    display: flex;
    align-items: center;
    gap: 10px;
}

.unit-toggle {
    display: flex;
    border: 1px solid var(--border-color);
    border-radius: 8px;
    overflow: hidden;
}

.unit-btn {
    padding: 8px 12px;
    border: none;
    background: #f1f5f9;
    cursor: pointer;
    transition: all 0.2s ease;
}

.unit-btn.active {
    background: var(--primary-color);
    color: white;
}

.unit-btn:hover {
    background: var(--secondary-color);
    color: white;
}
        :root {
            --primary-color: #4F46E5;
            --secondary-color: #6366F1;
            --accent-color: #818CF8;
            --background: #f8fafc;
            --text-color: #1e293b;
            --border-color: #e2e8f0;
            --gold-color: #E0C43D;
            --black-color: #000000;
            --brown-color: #8B4513;
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
            width: 80%;
            max-width: 400px;
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
            width: 25px;
            height: 25px;
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
        /* تنسيق إضافي */
#partTypeGroup {
    margin-top: 15px; /* تباعد بين الحقل والخيارات السابقة */
}
        /* تصميم زر تحميل الصور */
.upload-container {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
}
/* إطار الصورة الرئيسية */
.upload-box.main-image {
    border: 3px solid var(--primary-color);
    box-shadow: 0 4px 12px rgba(79, 70, 229, 0.25);
}

.main-image-box {
    width: 200px;
    height: 200px;
    border: 3px dashed var(--border-color);
    border-radius: 12px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s ease;
    background: var(--background);
    position: relative;
}
.main-image-box img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
}

.main-image-box i {
    font-size: 24px;
    color: var(--primary-color);
    margin-bottom: 10px;
}

.main-image-box p {
    margin: 0;
    font-size: 0.9rem;
    color: var(--text-color);
}

/* زر الحذف */
.remove-btn {
    position: absolute;
    top: 5px;
    right: 5px;
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
/* تنسيق إضافي */
#currencySymbol {
    font-size: 1.2rem;
    color: var(--primary-color);
    margin-left: 10px;
}
/* تحسين شكل الصور */
.upload-box img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
}
        .step-circle.active {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            box-shadow: 0 4px 12px rgba(79, 70, 229, 0.25);
            border-color: var(--primary-color);
        }
     .icon-option {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 10px;
    border: 2px solid var(--border-color);
        font-size: 0.8rem; /* تقليل حجم الخط */
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s ease;
    background: white;
    text-align: center;
}

.icon-option i {
    font-size: 24px;
    color: var(--primary-color);
    margin-bottom: 10px;
}

.icon-option:hover {
    border-color: var(--primary-color);
    background: rgba(79, 70, 229, 0.05);
}

.icon-option.active {
    border-color: var(--primary-color);
    background: rgba(79, 70, 229, 0.1);
}   
/* تصميم مربعات تحميل الصور */
.upload-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 15px;
    margin-top: 20px;
}

.upload-grid .upload-box {
    position: relative;
    border: 2px solid var(--border-color);
}

.upload-grid .upload-box img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
}

.upload-grid .remove-btn {
    position: absolute;
    top: 5px;
    right: 5px;
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

.upload-grid .set-main-btn {
    position: absolute;
    top: 5px;
    left: 5px;
    background: rgba(0, 123, 255, 0.8);
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

.upload-grid .set-main-btn.active {
    background: var(--primary-color);
}

.upload-box {
    width: 150px; /* حجم المربع */
    height: 150px; /* حجم المربع */
    border: 2px dashed var(--border-color);
    border-radius: 12px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s ease;
    background: var(--background);
}

.upload-box:hover {
    border-color: var(--primary-color);
    background: rgba(79, 70, 229, 0.05);
}

.upload-box i {
    font-size: 24px;
    color: var(--primary-color);
    margin-bottom: 10px;
}

.upload-box p {
    margin: 0;
    font-size: 0.9rem;
    color: var(--text-color);
}
/* تنسيق إضافي */
#saleCurrencySymbol,
.rentalCurrencySymbol {
    font-size: 1.2rem;
    color: var(--primary-color);
    margin-left: 10px;
}
/* تصميم الصور المضافة */
.upload-box img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
}

.upload-box .remove-btn {
    position: absolute;
    top: 5px;
    right: 5px;
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

.upload-box .set-main-btn {
    position: absolute;
    top: 5px;
    left: 5px;
    background: rgba(0, 123, 255, 0.8);
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

.upload-box .set-main-btn.active {
    background: var(--primary-color);
}

/* رسالة تحذير */
.warning-message {
    display: block;
    margin-top: 10px;
    font-size: 0.85rem;
    color: #dc3545;
    text-align: center;
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
    display: flex;
    flex-direction: column; /* ترتيب العناصر بشكل عمودي */
    gap: 10px; /* المسافة بين العناصر */
}

.input-group label {
    display: block;
    margin-bottom: 0px; /* زيادة المسافة بين التسمية والخيارات */
        margin-top: 15px; /* زيادة المسافة بين التسمية والخيارات */
    font-weight: 600; /* زيادة سماكة الخط */
    color: var(--text-color);
    font-size: 1rem; /* زيادة حجم الخط */
    text-align: right; /* توسيط النص */
    width: 100%; /* جعل العرض يتكيف مع الحاوية */
}

        .input-group label.required::after {
            content: " *";
            color: red;
        }

.input-group input,
.input-group select,
.input-group textarea {
    width: 90%; /* تقليل العرض */
    padding: 8px 10px; /* تقليل الحشو */
    border: 1.5px solid var(--border-color);
    border-radius: 8px;
    font-size: 0.8rem; /* تقليل حجم الخط */
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
    flex-wrap: wrap; /* السماح للعناصر بالانتقال لأسفل إذا لم يكن هناك مساحة كافية */
    gap: 10px; /* المسافة بين العناصر */
}

        .icon-option,
        .country-option,
        .region-option,
        .neighborhood-option {
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

        .icon-option:hover,
        .country-option:hover,
        .region-option:hover,
        .neighborhood-option:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .icon-option.active,
        .country-option.active,
        .region-option.active,
        .neighborhood-option.active {
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
            cursor: grab;
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
    flex-direction: column; /* ترتيب الأزرار بشكل عمودي */
    gap: 10px; /* المسافة بين الأزرار */
    margin-top: 20px;
}

.form-actions .btn {
    width: 100%; /* جعل الأزرار تأخذ العرض الكامل */
}

        .btn {
            padding: 8px 12px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
                font-size: 0.8rem; /* تقليل حجم الخط */
                    width: auto; /* جعل العرض يتكيف مع المحتوى */
            font-weight: 600;
            transition: all 0.2s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .btn:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .btn:active {
            transform: scale(0.95);
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
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

        .region-options,
        .neighborhood-options {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .region-option,
        .neighborhood-option {
            flex: 1 1 calc(33.333% - 10px);
            padding: 10px;
            border: 2px solid var(--border-color);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s ease;
            text-align: center;
        }

        .region-option.active,
        .neighborhood-option.active {
            border-color: var(--primary-color);
            background: rgba(79, 70, 229, 0.1);
        }

        #price {
            font-size: 1.2rem;
            padding: 15px;
            border: 2px solid var(--primary-color);
            border-radius: 10px;
            width: 100%;
        }

        #description {
            height: 120px;
            resize: vertical;
            font-size: 1rem;
            padding: 15px;
            border: 2px solid var(--primary-color);
            border-radius: 10px;
            width: 100%;
        }

        .price-group {
            display: flex;
            gap: 10px;
            margin-bottom: 10px;
        }

        .price-group input {
            flex: 1;
        }

        .warning-message {
            font-size: 0.9rem;
            color: #dc3545;
            margin-top: 10px;
            text-align: center;
        }

        .vip-package {
            background: var(--black-color);
            color: var(--gold-color);
            border: 2px solid var(--gold-color);
        }

        .vip-package h3 {
            color: var(--gold-color);
        }

        .vip-package small {
            color: var(--gold-color);
        }

        .vip-package span {
            color: var(--gold-color);
        }

        .vip-icon {
            font-size: 24px;
            color: var(--gold-color);
        }

        .coffee-package {
            background: var(--brown-color);
            color: white;
            border: 2px solid var(--brown-color);
        }

        .coffee-package h3 {
            color: white;
        }

        .coffee-package small {
            color: white;
        }

        .coffee-package span {
            color: white;
        }

        .icon-option img {
            width: 24px;
            height: 24px;
            margin-bottom: 10px;
        }

        /* تلميع الباقات المدفوعة */
        .icon-option.turbo,
        .icon-option.vip,
        .icon-option.coffee {
            animation: glow 2s infinite alternate;
        }

        @keyframes glow {
            0% {
                box-shadow: 0 0 10px rgba(79, 70, 229, 0.5);
            }
            100% {
                box-shadow: 0 0 20px rgba(79, 70, 229, 0.8);
            }
        }

        /* تحسين اختيار الألوان */
.color-options {
    display: flex;
    flex-wrap: wrap;
    gap: 20px; /* تقليل المسافة بين العناصر */
}

.color-option {
    width: 40px; /* تقليل حجم دوائر الألوان */
    height: 40px;
    font-size: 0.7rem; /* تقليل حجم النص */
}


.color-option.active {
    border: 4px solid var(--primary-color); /* حدود أكثر سماكة */
    box-shadow: 0 0 10px rgba(79, 70, 229, 0.5); /* ظل أكثر وضوحًا */
    transform: scale(1.1); /* تكبير الدائرة قليلاً عند التحديد */
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
            <div class="step-circle hidden" onclick="changeStep(9)">9</div> <!-- الخطوة 9 مخفية افتراضيًا -->
        </div>

        <!-- الخطوة 1: اختيار الدولة -->
        <div class="form-step active" id="step1">
            <div class="step-header">
                <h2>اختيار الدولة</h2>
            </div>
            
            <div class="input-group">
                <label class="required">الدولة</label>
                <div class="icon-options">
                    <div class="country-option" data-code="+971" onclick="selectCountry('الإمارات', this)">
                        <img src="https://flagcdn.com/ae.svg" class="country-flag" alt="علم الإمارات">
                        <span>الإمارات العربية المتحدة</span>
                    </div>
                    <div class="country-option" data-code="+966" onclick="selectCountry('السعودية', this)">
                        <img src="https://flagcdn.com/sa.svg" class="country-flag" alt="علم السعودية">
                        <span>المملكة العربية السعودية</span>
                    </div>
                    <div class="country-option" data-code="+968" onclick="selectCountry('عمان', this)">
                        <img src="https://flagcdn.com/om.svg" class="country-flag" alt="علم عمان">
                        <span>سلطنة عمان</span>
                    </div>
                </div>
                <small class="help-text">اختر الدولة التي تريد الإعلان فيها</small>
            </div>

            <div class="input-group">
                <label class="required">المنطقة</label>
                <div class="region-options">
                    <!-- سيتم تعبئة المناطق هنا -->
                </div>
                <small class="help-text">اختر المنطقة (يمكن اختيار منطقة واحدة )</small>
            </div>

            <div class="input-group" id="neighborhoodGroup">
                <label>الحي</label>
                <div class="neighborhood-options">
                    <!-- سيتم تعبئة الأحياء هنا -->
                </div>
                <small class="help-text">اختر الحي (اختياري)</small>
            </div>

            <div class="form-actions">
                <button class="btn btn-primary" onclick="nextStep(2)">التالي</button>
            </div>
        </div>

        <!-- الخطوة 2: نوع الإعلان -->
        <div class="form-step" id="step2">
            <div class="step-header">
                <h2>نوع الإعلان</h2>
            </div>
            
            <div class="input-group">
                <label class="required">اختر النوع</label>
                <div class="icon-options">
                    <div class="icon-option" data-type="car" onclick="selectVehicleType('car')">
                        <i class="fas fa-car"></i>
                        <span>سيارة</span>
                    </div>
                    <div class="icon-option" data-type="truck" onclick="selectVehicleType('truck')">
                        <i class="fas fa-truck"></i>
                        <span>مركبات ثقيلة</span>
                    </div>
                    <div class="icon-option" data-type="motorcycle" onclick="selectVehicleType('motorcycle')">
                        <i class="fas fa-motorcycle"></i>
                        <span>دراجة نارية</span>
                    </div>
                    <div class="icon-option" data-type="boat" onclick="selectVehicleType('boat')">
                        <i class="fas fa-ship"></i>
                        <span>قوارب</span>
                    </div>
                    <div class="icon-option" data-type="services" onclick="selectVehicleType('services')">
                        <i class="fas fa-tools"></i>
                        <span>خدمات المركبات</span>
                    </div>
                    <div class="icon-option" data-type="plates" onclick="selectVehicleType('plates')">
<i class="fa-solid fa-tachograph-digital"></i>
<span>لوحات المركبات</span>
                    </div>
                    <div class="icon-option" data-type="other" onclick="selectVehicleType('other')">
                        <i class="fas fa-ad"></i>
                        <span>إعلانات مبوبة أخرى</span>
                    </div>
                </div>
                <small class="help-text">اختر نوع الإعلان الذي تريد نشره</small>
            </div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(1)">السابق</button>
                <button class="btn btn-primary" onclick="nextStep(3)">التالي</button>
            </div>
        </div>
<!-- الخطوة 2.1: اختيار نوع الدراجة -->
<div class="form-step hidden" id="step2-1">
    <div class="step-header">
        <h2>اختر نوع الدراجة</h2>
    </div>
    
    <div class="input-group">
        <label>النوع</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectBikeType('برية')">
                <i class="fas fa-biking"></i>
                <span>دراجة برية</span>
            </div>
            <div class="icon-option" onclick="selectBikeType('مائية')">
                <i class="fas fa-water"></i>
                <span>دراجة مائية</span>
            </div>
        </div>
    </div>

    <div class="form-actions">
        <button class="btn btn-secondary" onclick="prevStep(2)">السابق</button>
        <button class="btn btn-primary" onclick="nextStep(3)">التالي</button>
    </div>
</div>

<!-- الخطوة 2.2: اختيار نوع المركبة الثقيلة -->
<div class="form-step hidden" id="step2-2">
    <div class="step-header">
        <h2>اختر نوع المركبة الثقيلة</h2>
    </div>
    
    <div class="input-group">
        <label>النوع</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectHeavyVehicleType('شاحنة')">
                <i class="fas fa-truck-moving"></i>
                <span>شاحنة</span>
            </div>
            <div class="icon-option" onclick="selectHeavyVehicleType('مقطورة')">
                <i class="fas fa-trailer"></i>
                <span>مقطورة</span>
            </div>
            <div class="icon-option" onclick="selectHeavyVehicleType('آليات بناء')">
                <i class="fas fa-tools"></i>
                <span>آليات بناء</span>
            </div>
        </div>
    </div>

    <div class="form-actions">
        <button class="btn btn-secondary" onclick="prevStep(2)">السابق</button>
        <button class="btn btn-primary" onclick="nextStep(3)">التالي</button>
    </div>
</div>


<!-- خدمات المركبات (step2-3) -->
<div class="form-step hidden" id="step2-3">
    <div class="step-header">
        <h2>اختر نوع الخدمة</h2>
    </div>
    
    
        
    <div class="input-group">
        <label>الخدمة</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectServiceType('غسيل والعناية')">
<i class="fa-solid fa-car-tunnel"></i>
<span>غسيل وعناية بالمركبات</span>
            </div>
            <div class="icon-option" onclick="selectServiceType('رخص تجارية')">
                <i class="fas fa-file-contract"></i>
                <span>رخص تجارية</span>
            </div>
            <div class="icon-option" onclick="selectServiceType('صيانة المركبات')">
                <i class="fas fa-tools"></i>
                <span>صيانة المركبات</span>
            </div>
            <div class="icon-option" onclick="selectServiceType('شراء المركبات')">
<i class="fa-solid fa-comments-dollar"></i>                <span>شراء المركبات</span>
            </div>
            <div class="icon-option" onclick="selectServiceType('تأمين المركبات')">
                <i class="fas fa-shield-alt"></i>
                <span>تأمين المركبات</span>
            </div>
            <div class="icon-option" onclick="selectServiceType('قطر وشحن المركبات')">
<i class="fa-solid fa-truck-plane"></i> 
<span>قطر وشحن المركبات</span>
            </div>
            <div class="icon-option" onclick="selectServiceType('فحص المركبات')">
<i class="fa-solid fa-screwdriver"></i>
<span>فحص المركبات</span>
            </div>
        </div>
        </div>

    
    
            <div class="input-group">
            <label class="required">السعر المطلوب</label>
            <div style="display: flex; align-items: center; gap: 10px;">
                <input type="number" id="price" placeholder="أدخل السعر المطلوب" required>
                <span id="saleCurrencySymbol" style="font-weight: bold;">AED</span> <!-- رمز العملة للبيع -->
            </div>
        </div>

        <div class="input-group">
            <div class="icon-options compact">
                <div class="icon-option small" onclick="toggleNegotiable(this)">
                    <i class="fas fa-handshake"></i>
                    <span>قابل للتفاوض</span>
                </div>
                <div class="icon-option small" onclick="toggleUrgentSale(this)">
                    <i class="fas fa-bolt"></i>
                    <span>بيعة مستعجلة</span>
                </div>
                            </div>
                                </div>

                        <div class="input-group">
    <label class="required">طريقة الدفع</label>
    <div class="icon-options">
        <div class="icon-option" onclick="togglePaymentMethod('كاش', this)">
            <i class="fas fa-money-bill-wave"></i>
            <span>كاش</span>
        </div>
        <div class="icon-option" onclick="togglePaymentMethod('اقساط', this)">
            <i class="fas fa-credit-card"></i>
            <span>اقساط</span>
        </div>
    </div>
            </div>
    <!-- حقل رقم الهاتف -->
    <div class="input-group">
        <label class="required">رقم الهاتف</label>
        <div style="display: flex; gap: 10px; align-items: center;">
            <input type="tel" id="phoneServices" style="flex: 1; padding: 15px; font-size: 16px; border: 2px solid #ccc; border-radius: 8px; direction: ltr;" required>
            <input type="text" id="countryCodeServices" style="flex: 0 0 80px; background: #f1f5f9; text-align: center; padding: 15px; font-size: 20px; border: 3px solid #ccc; border-radius: 8px; direction: ltr;" readonly>
        </div>
        <small class="help-text">سيتم استخدام هذا الرقم للتواصل معك</small>
    </div>

    <!-- رقم الواتساب -->
    <div class="input-group">
        <label>رقم الواتساب (اختياري)</label>
        <div style="display: flex; gap: 10px; align-items: center;">
            <i class="fab fa-whatsapp" style="font-size: 24px; color: #25D366;"></i>
            <input type="tel" id="whatsapp" style="flex: 1; padding: 15px; font-size: 16px; border: 2px solid #ccc; border-radius: 8px; direction: ltr;">
        </div>
    </div>

    <!-- صندوق الوصف -->
    <div class="input-group">
        <label class="required">الوصف</label>
        <textarea id="description" placeholder="أدخل وصفًا للإعلان" style="height: 120px; resize: vertical; font-size: 1rem; padding: 15px; border: 2px solid var(--primary-color); border-radius: 5px; width: 100%;"></textarea>
        <small class="warning-message">نصيحة: قم بمقابلة المشتري في مكان عام ولا ترسل أي عربون أو رسوم لشركة توصيل.</small>
    </div>

    <div class="form-actions">
        <button class="btn btn-secondary" onclick="prevStep(2)">السابق</button>
        <button class="btn btn-primary" onclick="nextStep(4)">التالي</button>
    </div>
        </div>


<!-- لوحات المركبات (step2-4) -->
<div class="form-step hidden" id="step2-4">
    <div class="step-header">
        <h2>تفاصيل لوحات المركبات</h2>
    </div>
    
    
        
    <!-- نوع الإعلان -->
    <div class="input-group">
        <label class="required">نوع الإعلان</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectAdType1('بيع', this)">
                <i class="fas fa-hand-holding-usd"></i>
                <span>بيع</span>
            </div>
            <div class="icon-option" onclick="selectAdType1('مطلوب للشراء', this)">
                <i class="fas fa-search-dollar"></i>
                <span>مطلوب للشراء</span>
            </div>
        </div>
    </div>

    <!-- نوع اللوحة -->
    <div class="input-group">
        <label class="required">نوع اللوحة</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectPlateType('سيارة', this)">
                <i class="fas fa-car"></i>
                <span>سيارة</span>
            </div>
            <div class="icon-option" onclick="selectPlateType('دراجة', this)">
                <i class="fas fa-motorcycle"></i>
                <span>دراجة</span>
            </div>
            <div class="icon-option" onclick="selectPlateType('أخرى', this)">
                <i class="fas fa-ad"></i>
                <span>أخرى</span>
            </div>
        </div>
    </div>

    <!-- هل اللوحة خصوصي أو كلاسيكي -->
    <div class="input-group">
        <label class="required">هل اللوحة خصوصي أو كلاسيكي؟</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectPlateCategory('خصوصي', this)">
                <i class="fas fa-id-card"></i>
                <span>خصوصي</span>
            </div>
            <div class="icon-option" onclick="selectPlateCategory('كلاسيكي', this)">
                <i class="fas fa-id-card-alt"></i>
                <span>كلاسيكي</span>
            </div>
        </div>
    </div>

    <!-- هل اللوحة مسجلة أم لا -->
    <div class="input-group">
        <label class="required">هل اللوحة مسجلة؟</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectPlateRegistration('مسجلة', this)">
                <i class="fas fa-check-circle"></i>
                <span>مسجلة</span>
            </div>
            <div class="icon-option" onclick="selectPlateRegistration('غير مسجلة', this)">
                <i class="fas fa-times-circle"></i>
                <span>غير مسجلة</span>
            </div>
        </div>
    </div>

    <!-- هل اللوحة من المالك مباشرة -->
    <div class="input-group">
        <label class="required">هل اللوحة من المالك مباشرة؟</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectPlateOwnership('نعم', this)">
                <i class="fas fa-check-circle"></i>
                <span>نعم</span>
            </div>
            <div class="icon-option" onclick="selectPlateOwnership('لا', this)">
                <i class="fas fa-times-circle"></i>
                <span>لا</span>
            </div>
        </div>
    </div>

    <!-- كود اللوحة ومصدرها -->
    <div class="input-group">
        <label class="required">كود اللوحة ومصدرها</label>
        <textarea id="plateDetails" placeholder="أدخل كود اللوحة ومصدرها (مثال: لوحة دبي، كود 1234)" class="plate-input"></textarea>
    </div>

    
            <div class="input-group">
            <label class="required">السعر المطلوب</label>
            <div style="display: flex; align-items: center; gap: 10px;">
                <input type="number" id="price" placeholder="أدخل السعر المطلوب" required>
                <span id="saleCurrencySymbol" style="font-weight: bold;">AED</span> <!-- رمز العملة للبيع -->
            </div>
        </div>

        <div class="input-group">
            <div class="icon-options compact">
                <div class="icon-option small" onclick="toggleNegotiable(this)">
                    <i class="fas fa-handshake"></i>
                    <span>قابل للتفاوض</span>
                </div>
                <div class="icon-option small" onclick="toggleUrgentSale(this)">
                    <i class="fas fa-bolt"></i>
                    <span>بيعة مستعجلة</span>
                </div>
                            </div>
                                </div>

                        <div class="input-group">
    <label class="required">طريقة الدفع</label>
    <div class="icon-options">
        <div class="icon-option" onclick="togglePaymentMethod('كاش', this)">
            <i class="fas fa-money-bill-wave"></i>
            <span>كاش</span>
        </div>
        <div class="icon-option" onclick="togglePaymentMethod('اقساط', this)">
            <i class="fas fa-credit-card"></i>
            <span>اقساط</span>
        </div>
    </div>
</div>
    <!-- حقل رقم الهاتف -->
    <div class="input-group">
        <label class="required">رقم الهاتف</label>
        <div style="display: flex; gap: 10px; align-items: center;">
            <input type="tel" id="phonePlates" style="flex: 1; padding: 15px; font-size: 16px; border: 2px solid #ccc; border-radius: 8px; direction: ltr;" required>
            <input type="text" id="countryCodePlates" style="flex: 0 0 80px; background: #f1f5f9; text-align: center; padding: 15px; font-size: 20px; border: 3px solid #ccc; border-radius: 8px; direction: ltr;" readonly>
        </div>
        <small class="help-text">سيتم استخدام هذا الرقم للتواصل معك</small>
    </div>

    <!-- رقم الواتساب -->
    <div class="input-group">
        <label>رقم الواتساب (اختياري)</label>
        <div style="display: flex; gap: 10px; align-items: center;">
            <i class="fab fa-whatsapp" style="font-size: 24px; color: #25D366;"></i>
            <input type="tel" id="whatsapp" style="flex: 1; padding: 15px; font-size: 16px; border: 2px solid #ccc; border-radius: 8px; direction: ltr;">
        </div>
    </div>

    <!-- صندوق الوصف -->
    <div class="input-group">
        <label class="required">الوصف</label>
        <textarea id="description" placeholder="أدخل وصفًا للإعلان" style="height: 120px; resize: vertical; font-size: 1rem; padding: 15px; border: 2px solid var(--primary-color); border-radius: 5px; width: 100%;"></textarea>
        <small class="warning-message">نصيحة: قم بمقابلة المشتري في مكان عام ولا ترسل أي عربون أو رسوم لشركة توصيل.</small>
    </div>


    <div class="form-actions">
        <button class="btn btn-secondary" onclick="prevStep(2)">السابق</button>
        <button class="btn btn-primary" onclick="nextStep(3)">التالي</button>
    </div>
</div>



<!-- الخطوة 3-special -->
<div class="form-step" id="step3-special">
    <div class="step-header">
        
        <h2>تفاصيل الاتصال</h2>
    </div>


        <div class="input-group">
            <label class="required">السعر المطلوب</label>
            <div style="display: flex; align-items: center; gap: 10px;">
                <input type="number" id="price" placeholder="أدخل السعر المطلوب" required>
                <span id="saleCurrencySymbol" style="font-weight: bold;">AED</span> <!-- رمز العملة للبيع -->
            </div>
        </div>

        <div class="input-group">
            <div class="icon-options compact">
                <div class="icon-option small" onclick="toggleNegotiable(this)">
                    <i class="fas fa-handshake"></i>
                    <span>قابل للتفاوض</span>
                </div>
                <div class="icon-option small" onclick="toggleUrgentSale(this)">
                    <i class="fas fa-bolt"></i>
                    <span>بيعة مستعجلة</span>
                </div>
                            </div>
                                </div>

                        <div class="input-group">
    <label class="required">طريقة الدفع</label>
    <div class="icon-options">
        <div class="icon-option" onclick="togglePaymentMethod('كاش', this)">
            <i class="fas fa-money-bill-wave"></i>
            <span>كاش</span>
        </div>
        <div class="icon-option" onclick="togglePaymentMethod('اقساط', this)">
            <i class="fas fa-credit-card"></i>
            <span>اقساط</span>
        </div>
    </div>
</div>



    <!-- رقم الهاتف -->
    <div class="input-group">
        <label class="required">رقم الهاتف</label>
        <div style="display: flex; gap: 10px; align-items: center;">
            <input type="tel" id="phoneSpecial" style="flex: 1; padding: 15px; font-size: 16px; border: 2px solid #ccc; border-radius: 8px; direction: ltr;" required>
            <input type="text" id="countryCodeSpecial" style="flex: 0 0 80px; background: #f1f5f9; text-align: center; padding: 15px; font-size: 20px; border: 3px solid #ccc; border-radius: 8px; direction: ltr;" readonly>
        </div>
        <small class="help-text">سيتم استخدام هذا الرقم للتواصل معك</small>
    </div>

    <!-- رقم الواتساب -->
    <div class="input-group">
        <label>رقم الواتساب (اختياري)</label>
        <div style="display: flex; gap: 10px; align-items: center;">
            <i class="fab fa-whatsapp" style="font-size: 24px; color: #25D366;"></i>
            <input type="tel" id="whatsapp" style="flex: 1; padding: 15px; font-size: 16px; border: 2px solid #ccc; border-radius: 8px; direction: ltr;">
        </div>
    </div>

    <!-- صندوق الوصف -->
    <div class="input-group">
        <label class="required">الوصف</label>
        <textarea id="description" placeholder="أدخل وصفًا للإعلان" style="height: 120px; resize: vertical; font-size: 1rem; padding: 15px; border: 2px solid var(--primary-color); border-radius: 5px; width: 100%;"></textarea>
        <small class="warning-message">نصيحة: قم بمقابلة المشتري في مكان عام ولا ترسل أي عربون أو رسوم لشركة توصيل.</small>
    </div>

    <div class="form-actions">
        <button class="btn btn-secondary" onclick="prevStep(2)">السابق</button>
        <button class="btn btn-primary" onclick="nextStep(6)">التالي</button>
    </div>
</div>

<!-- الخطوة 3: إختيارات سريعة -->
<div class="form-step" id="step3">
    <div class="step-header">
        <h2>إختيارات سريعة</h2>
    </div>
    <!-- 1- هل الإعلان بيع أو إيجار؟ -->
    <div class="input-group">
        <label class="required">نوع الإعلان</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectAdType('بيع', this)">
                <i class="fas fa-hand-holding-usd"></i>
                <span>بيع</span>
            </div>
            <div class="icon-option" onclick="selectAdType('إيجار', this)">
                <i class="fas fa-file-contract"></i>
                <span>إيجار</span>
            </div>
            <div class="icon-option" onclick="selectAdType('مطلوب للشراء', this)">
                <i class="fas fa-search-dollar"></i>
                <span>مطلوب للشراء</span>
            </div>
        </div>
    </div>

    <!-- 2- هل المركبة جديدة أو مستعملة؟ -->
    <div class="input-group">
        <label class="required">حالة المركبة</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectOption(this, 'vehicleCondition', 'جديدة')">
                <i class="fa-solid fa-car-on"></i>
                <span>جديدة</span>
            </div>
            <div class="icon-option" onclick="selectOption(this, 'vehicleCondition', 'مستعملة')">
                <i class="fa-solid fa-car"></i>
                <span>مستعملة</span>
            </div>
            <div class="icon-option" id="accidentOption" onclick="selectOption(this, 'vehicleCondition', 'حادث/سكراب')">
                <i class="fas fa-car-crash"></i>
                <span>حادث/سكراب</span>
            </div>
        </div>
    </div>

    <!-- 3- هل تريد نشر مركبة أو قطع غيارها أو اكسسوارات خاصة بها؟ -->
    <div class="input-group" id="adCategoryGroup">
        <label class="required">نوع السلعة</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectOption(this, 'adCategory', 'مركبة')">
                <i class="fa-solid fa-car-side"></i>
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

    <!-- 4- هل القطعة أصلية أو تجارية؟ (يظهر فقط عند اختيار قطع غيار أو اكسسوارات) -->
    <div class="input-group" id="partTypeGroup" style="display: none;">
        <label class="required">هل القطعة أصلية أو تجارية؟</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectOption(this, 'partType', 'أصلية')">
                <i class="fas fa-check-circle"></i>
                <span>أصلية</span>
            </div>
            <div class="icon-option" onclick="selectOption(this, 'partType', 'تجارية')">
                <i class="fas fa-times-circle"></i>
                <span>تجارية</span>
            </div>
        </div>
    </div>
    
            <!-- 5- هل عليها ضمان؟ -->
            <div class="input-group">
                <label class="required">هل عليها ضمان؟</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'warranty', 'نعم')">
                        <i class="fas fa-check-circle"></i>
                        <span>نعم</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'warranty', 'لا')">
                        <i class="fas fa-times-circle"></i>
                        <span>لا</span>
                    </div>
                </div>
            </div>
            
            <!-- 5.1- كم باقي على الضمان؟ -->
            <div class="input-group" id="warrantyDurationGroup">
                <label>كم باقي على الضمان؟ (اختياري)</label>
                <input type="text" id="warrantyDuration" placeholder="أدخل المدة المتبقية">
            </div>
            
            <!-- 6- هل المركبة للتصدير فقط أو للتصدير والاستخدام؟ -->
            <div class="input-group" id="exportGroup">
                <label class="required">نوع العرض</label>
                <div class="icon-options">
                                        <div class="icon-option" onclick="selectOption(this, 'exportType', 'أستخدام وتصدير')">
                        <i class="fas fa-globe-americas"></i>
                        <span>أستخدام وتصدير</span>
                                            </div>
                    <div class="icon-option" onclick="selectOption(this, 'exportType', 'تصدير فقط')">
                        <i class="fas fa-globe"></i>
                        <span>تصدير فقط</span>
                    </div>
                </div>
            </div>

            <!-- 7- هل المركبة مسجلة داخل الدولة أو لا؟ -->
            <div class="input-group" id="registrationGroup">
                <label class="required">حالة التسجيل</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'registration', 'مسجلة')">
                        <i class="fas fa-check-circle"></i>
                        <span>مسجلة</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'registration', 'غير مسجلة')">
                        <i class="fas fa-times-circle"></i>
                        <span>غير مسجلة</span>
                    </div>
                                        <div class="icon-option" onclick="selectOption(this, 'registration', 'قيد التسجيل')">
                        <i class="fas fa-circle"></i>
                        <span>قيد التسجيل</span>
                                           </div>
                </div>
            </div>

            <!-- 8- مواصفات المركبة -->
            <div class="input-group">
                <label class="required">مواصفات الاقليمية</label>
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
                    <div class="icon-option" onclick="selectOption(this, 'specifications', 'أوروبية')">
                        <i class="fas fa-flag-eu"></i>
                        <span>أوروبية</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'specifications', 'كورية')">
                        <i class="fas fa-flag-ko"></i>
                        <span>كورية</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'specifications', 'يابانية')">
                        <i class="fas fa-flag-ja"></i>
                        <span>يابانية</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'specifications', 'أخرى')">
                        <i class="fas fa-ellipsis-h"></i>
                        <span>أخرى</span>
                    </div>
                </div>
            </div>

            <!-- 9- نوع ناقل الحركة -->
            <div class="input-group">
                <label class="required">نوع ناقل الحركة</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'transmission', 'عادي')">
                        <i class="fas fa-cogs"></i>
                        <span>عادي</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'transmission', 'أوتوماتيك')">
                        <i class="fas fa-cog"></i>
                        <span>أوتوماتيك</span>
                    </div>
                </div>
            </div>

            <!-- 10- نوع الوقود -->
            <div class="input-group">
                <label class="required">نوع الوقود</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'fuelType', 'بنزين')">
                        <i class="fas fa-gas-pump"></i>
                        <span>بنزين</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'fuelType', 'ديزل')">
                        <i class="fas fa-truck-moving"></i>
                        <span>ديزل</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'fuelType', 'هايبرد')">
                        <i class="fas fa-car-battery"></i>
                        <span>هايبرد</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'fuelType', 'كهرباء')">
                        <i class="fas fa-bolt"></i>
                        <span>كهرباء</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'fuelType', 'غاز')">
                        <i class="fas fa-fire"></i>
                        <span>غاز</span>
                    </div>
                </div>
            </div>

            <!-- 11- أنظمة الدفع -->
            <div class="input-group">
                <label class="required">نظام الدفع</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', 'دفع أمامي')">
                        <i class="fas fa-car-side"></i>
                        <span>دفع أمامي</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', 'دفع خلفي')">
                        <i class="fas fa-car-side"></i>
                        <span>دفع خلفي</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', 'دفع رباعي (4×4)')">
                        <i class="fas fa-car-side"></i>
                        <span>دفع رباعي (4×4)</span>
                    </div>
                </div>
            </div>


    <!-- 12- عدد الاسطوانات -->
            <div class="input-group">
                <label class="required">عدد الأسطوانات</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', '3')">
                        <span>3</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', '4')">
                        <span>4</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', '6')">
                        <span>6</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', '8')">
                        <span>8</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', '10')">
                        <span>10</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', '12')">
                        <span>12</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', '16')">
                        <span>16</span>
                                            </div>
                    <div class="icon-option" onclick="selectOption(this, 'driveSystem', 'أخرى')">
                        <span>أخرى</span>
                    </div>
                </div>
            </div>
    <!-- 13- عدد الأحصنة -->
<div class="input-group">
    <label class="required">عدد الأحصنة</label>
    <select id="horsepower" required>
        <option value="" disabled selected>اختر عدد الأحصنة</option>
        <option value="70-150">70 - 150 حصان</option>
        <option value="150-250">150 - 250 حصان</option>
        <option value="250-450">250 - 450 حصان</option>
        <option value="450-700">450 - 700 حصان</option>
        <option value="700-1500+">700 - 1500+ حصان</option>
        <option value="other">أخرى</option>
    </select>
</div>
    <!-- 14- حجم المحرك -->
<!-- في الخطوة 3 أو الخطوة المناسبة -->
<div class="input-group">
    <label class="required">حجم المحرك</label>
    <div style="display: flex; gap: 20px;">
        <!-- سعات المحرك التقليدية (CC) -->
        <div style="flex: 1;">
            <label>سعات المحرك (CC)</label>
            <select id="engineSizeCC" required>
                <option value="" disabled selected>اختر سعة المحرك</option>
                <option value="1000-1600">1000 - 1600 CC</option>
                <option value="1600-2500">1600 - 2500 CC</option>
                <option value="2500-4000">2500 - 4000 CC</option>
                <option value="4000-6000">4000 - 6000 CC</option>
                <option value="6000+">6000 CC وأكثر</option>
                <option value="other">أخرى</option>
            </select>
        </div>

        <!-- سعات المحرك الكهربائي (kW) -->
        <div style="flex: 1;">
            <label>سعات المحرك الكهربائي (kW)</label>
            <select id="engineSizeKW" required>
                <option value="" disabled selected>اختر سعة المحرك الكهربائي</option>
                <option value="50-100">50 - 100 kW</option>
                <option value="100-250">100 - 250 kW</option>
                <option value="250-500">250 - 500 kW</option>
                <option value="500-1000">500 - 1000 kW</option>
                <option value="1000+">1000 kW وأكثر</option>
                <option value="other">أخرى</option>
            </select>
        </div>
    </div>
</div>
            <!-- 15- هل هي من المالك مباشرة؟ -->
            <div class="input-group">
                <label class="required">هل هي من المالك مباشرة؟</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'directOwner', 'نعم')">
                        <i class="fas fa-check-circle"></i>
                        <span>نعم</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'directOwner', 'لا')">
                        <i class="fas fa-times-circle"></i>
                        <span>لا</span>
                    </div>
                </div>
            </div>

            <!-- 17- مواصفات المركبة (كاملة، نصف مواصفات، عادية) -->
            <div class="input-group">
                <label class="notrequired">مواصفات المركبة</label>
                <div class="icon-options">
                    <div class="icon-option" onclick="selectOption(this, 'specificationsLevel', 'كاملة المواصفات')">
<i class="fa-solid fa-star"></i>

<span>كاملة المواصفات</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'specificationsLevel', 'نصف مواصفات')">
                        <i class="fas fa-star-half-alt"></i>
                        <span>نصف مواصفات</span>
                    </div>
                    <div class="icon-option" onclick="selectOption(this, 'specificationsLevel', 'إعتيادية')">
                    <i class="fa-regular fa-star"></i>

                        <span>إعتيادية</span>
                    </div>
                </div>
            </div>

            <!-- 18- اختيارات صغيرة للمركبات -->
            <div class="input-group" id="vehicleTypeGroup">
                <label class="notrequired">صنف الإعلان </label>
                <div class="icon-options">
                    <div class="icon-option" onclick="toggleOption(this, 'economical')">
                        <i class="fas fa-gas-pump"></i>
                        <span>اقتصادية وعملية</span>
                    </div>
                    <div class="icon-option" onclick="toggleOption(this, 'sporty')">
                        <i class="fas fa-tachometer-alt"></i>
                        <span>رياضية وشبابية</span>
                    </div>
                    <div class="icon-option" onclick="toggleOption(this, 'luxury')">
                        <i class="fas fa-gem"></i>
                        <span>كشخة وكبار الشخصيات</span>
                    </div>
                    <div class="icon-option" onclick="toggleOption(this, 'adventure')">
                        <i class="fas fa-hiking"></i>
                        <span>كشتات ومغامرات</span>
                    </div>
                    <div class="icon-option" onclick="toggleOption(this, 'family')">
                        <i class="fas fa-users"></i>
                        <span>عائلية وكبيرة</span>
                    </div>
                    <div class="icon-option" onclick="toggleOption(this, 'family')">
<i class="fa-solid fa-person-cane"></i>
<span>كلاسيكية ونادرة</span>
                    </div>
                    <div class="icon-option" onclick="toggleOption(this, 'pickup')">
                        <i class="fas fa-truck-pickup"></i>
                        <span>بيك أب وتحميل</span>
                    </div>
                </div>
            </div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(2)">السابق</button>
                <button class="btn btn-primary" onclick="nextStep(4)">التالي</button>
            </div>
        </div>
        <!-- الخطوة 4: تفاصيل المركبة -->
<div class="form-step" id="step4">
    <div class="step-header">
        <h2>تفاصيل المركبة</h2>
    </div>

    <!-- تفاصيل المركبة -->
    <div id="dynamicContent"></div>
    
    <!-- تفاصيل البيع -->
    <div id="saleDetails" class="hidden">
        <div class="input-group">
            <label class="required">السعر المطلوب</label>
            <div style="display: flex; align-items: center; gap: 10px;">
                <input type="number" id="price" placeholder="أدخل السعر المطلوب" required>
                <span id="saleCurrencySymbol" style="font-weight: bold;">AED</span> <!-- رمز العملة للبيع -->
            </div>
        </div>

        <div class="input-group">
            <div class="icon-options compact">
                <div class="icon-option small" onclick="toggleNegotiable(this)">
                    <i class="fas fa-handshake"></i>
                    <span>قابل للتفاوض</span>
                </div>
                <div class="icon-option small" onclick="toggleUrgentSale(this)">
                    <i class="fas fa-bolt"></i>
                    <span>بيعة مستعجلة</span>
                </div>
                            </div>
                                </div>

                        <div class="input-group">
    <label class="required">طريقة الدفع</label>
    <div class="icon-options">
        <div class="icon-option" onclick="togglePaymentMethod('كاش', this)">
            <i class="fas fa-money-bill-wave"></i>
            <span>كاش</span>
        </div>
        <div class="icon-option" onclick="togglePaymentMethod('اقساط', this)">
            <i class="fas fa-credit-card"></i>
            <span>اقساط</span>
        </div>
    </div>
</div>
</div>

    <!-- تفاصيل الإيجار -->
    <div id="rentalDetails" class="hidden">
<!-- داخل الخطوة 4 -->
<div class="input-group">
    <label class="required">أسعار الإيجار والتأمين</label>
    <table class="price-table">
        <thead>
            <tr>
                <th>أسعار الإيجار</th> <!-- تم تبديل العناوين -->
                <th>أسعار التأمين</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <input type="number" id="dailyRent" placeholder="يومي">
                        <span class="rentalCurrencySymbol" style="font-weight: bold;">AED</span>
                    </div>
                </td>
                <td>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <input type="number" id="dailyInsurance" placeholder="يومي">
                        <span class="rentalCurrencySymbol" style="font-weight: bold;">AED</span>
                    </div>
                </td>
            </tr>
            <tr>
                <td>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <input type="number" id="weeklyRent" placeholder="أسبوعي">
                        <span class="rentalCurrencySymbol" style="font-weight: bold;">AED</span>
                    </div>
                </td>
                <td>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <input type="number" id="weeklyInsurance" placeholder="أسبوعي">
                        <span class="rentalCurrencySymbol" style="font-weight: bold;">AED</span>
                    </div>
                </td>
            </tr>
            <tr>
                <td>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <input type="number" id="monthlyRent" placeholder="شهري">
                        <span class="rentalCurrencySymbol" style="font-weight: bold;">AED</span>
                    </div>
                </td>
                <td>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <input type="number" id="monthlyInsurance" placeholder="شهري">
                        <span class="rentalCurrencySymbol" style="font-weight: bold;">AED</span>
                    </div>
                </td>
            </tr>
            <tr>
                <td>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <input type="number" id="yearlyRent" placeholder="سنوي">
                        <span class="rentalCurrencySymbol" style="font-weight: bold;">AED</span>
                    </div>
                </td>
                <td>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <input type="number" id="yearlyInsurance" placeholder="سنوي">
                        <span class="rentalCurrencySymbol" style="font-weight: bold;">AED</span>
                    </div>
                </td>
            </tr>
        </tbody>
    </table>
                        </div>

        <div class="input-group">
    <label class="required">طريقة الدفع</label>
    <div class="icon-options">
        <div class="icon-option" onclick="togglePaymentMethod('كاش', this)">
            <i class="fas fa-money-bill-wave"></i>
            <span>كاش</span>
        </div>
        <div class="icon-option" onclick="togglePaymentMethod('اقساط', this)">
            <i class="fas fa-credit-card"></i>
            <span>اقساط</span>
        </div>
    </div>
</div>
</div>

    <!-- رقم الهاتف -->
    <div class="input-group">
        <label class="required">رقم الهاتف</label>
        <div style="display: flex; gap: 10px; align-items: center;">
                        <input type="tel" id="phone" style="flex: 1; padding: 15px; font-size: 16px; border: 2px solid #ccc; border-radius: 8px; direction: ltr;" required>
            <input type="text" id="countryCode" style="flex: 0 0 80px; background: #f1f5f9; text-align: center; padding: 15px; font-size: 20px; border: 3px solid #ccc; border-radius: 8px; direction: ltr;" readonly>
        </div>
        <small class="help-text">سيتم استخدام هذا الرقم للتواصل معك</small>
    </div>

    <!-- رقم الواتساب -->
    <div class="input-group">
        <label>رقم الواتساب (اختياري)</label>
        <div style="display: flex; gap: 10px; align-items: center;">
            <i class="fab fa-whatsapp" style="font-size: 24px; color: #25D366;"></i>
            <input type="tel" id="whatsapp" style="flex: 1; padding: 15px; font-size: 16px; border: 2px solid #ccc; border-radius: 8px; direction: ltr;">
        </div>
    </div>

    <!-- صندوق الوصف -->
    <div class="input-group">
        <label class="required">الوصف</label>
        <textarea id="description" placeholder="أدخل وصفًا للإعلان" style="height: 120px; resize: vertical; font-size: 1rem; padding: 15px; border: 2px solid var(--primary-color); border-radius: 10px; width: 100%;"></textarea>
        
        <div class="input-group">
    <label>رقم الشاسيه (اختياري)</label>
    <input type="text" id="chassisNumber" placeholder="أدخل رقم الشاسيه">
</div>

<div class="input-group">
    <label>هل توجد مشكلة أو علامة في المركبة؟ (يمكن اختيار أكثر من خيار)</label>
    <div class="icon-options">
        <!-- خيار "لا" -->
        <div class="icon-option" onclick="toggleProblem('لا', this)">
<i class="fa-solid fa-circle-check" style="color: #63E6BE;"></i>            <span>لا</span>
        </div>
        <!-- خيار "علامة المحرك (Check Engine)" -->
        <div class="icon-option" onclick="toggleProblem('علامة المحرك (Check Engine)', this)">
<i class="fa-solid fa-cash-register" style="color: #FFD43B;"></i>            <span>علامة المحرك</span>
        </div>
        <!-- خيار "علامة الزيت" -->
        <div class="icon-option" onclick="toggleProblem('علامة الزيت', this)">
<i class="fa-solid fa-oil-can" style="color: #FFD43B;"></i>            <span>علامة الزيت</span>
        </div>
        <!-- خيار "علامة البطارية" -->
        <div class="icon-option" onclick="toggleProblem('علامة البطارية', this)">
<i class="fa-solid fa-car-battery" style="color: #FFD43B;"></i>            <span>علامة البطارية</span>
        </div>
        <!-- خيار "علامة الحرارة" -->
        <div class="icon-option" onclick="toggleProblem('علامة الحرارة', this)">
<i class="fa-solid fa-temperature-high" style="color: #FFD43B;"></i>            <span>علامة الحرارة</span>
        </div>
        <!-- خيار "علامة المكابح (Brake)" -->
        <div class="icon-option" onclick="toggleProblem('علامة المكابح (Brake)', this)">
            <span>علامة المكابح BRAKE</span>
        </div>
        <!-- خيار "علامة ABS" -->
        <div class="icon-option" onclick="toggleProblem('علامة ABS', this)">
<span>علامة ABS</span>
        </div>
        <!-- خيار "علامة الأيرباق" -->
        <div class="icon-option" onclick="toggleProblem('علامة الأيرباق', this)">
<i class="fa-solid fa-location-pin fa-rotate-270" style="color: #FFD43B;"></i>            <span>علامة الأيرباق</span>
        </div>
        <!-- خيار "علامة البنزين" -->
        <div class="icon-option" onclick="toggleProblem('علامة البنزين', this)">
<i class="fa-solid fa-gas-pump" style="color: #FFD43B;"></i>            <span>علامة البنزين</span>
        </div>
        <!-- خيار "علامة ضغط الإطارات (TPMS)" -->
        <div class="icon-option" onclick="toggleProblem('علامة ضغط الإطارات (TPMS)', this)">
<FontAwesomeIcon icon="fa-solid fa-circle-exclamation" style={{color: "#FFD43B",}} />
<span>علامة ضغط الإطارات</span>
        </div>
        <!-- خيار "علامة التوجيه (EPS/Steering)" -->
        <div class="icon-option" onclick="toggleProblem('علامة التوجيه (EPS/Steering)', this)">
            <i class="fas fa-steering-wheel"></i>
            <span>علامة التوجيه EPS</span>
        </div>
        <!-- خيار "أخرى" -->
        <div class="icon-option" onclick="toggleProblem('أخرى', this)">
            <i class="fas fa-ellipsis-h"></i>
            <span>أخرى</span>
        </div>
    </div>
</div>

        
        <div class="review-card warning">
    <h3><i class="fas fa-exclamation-triangle"></i> ملاحظات مهمة</h3>
    <ul class="warning-list">
        <li>ألتقي مع المشتري في مكان عام</li>
        <li>لا تأخذ عربون او تحويل بنكي تأكد قبل استلام اموالك</li>
            <li>لا تتعامل مع شركات التوصيل او تحويل لهم مبالغ مالية</li>
    </ul>
</div>

<style>
.review-card.warning {
    border-left: 4px solid #ffc107;
    background: #fff9e6;
}

.warning-list {
    list-style: none;
    padding: 0;
    color: #856404;
}

.warning-list li {
    padding: 5px 0;
    display: flex;
    align-items: center;
    gap: 8px;
}
</style>
    </div>

    <div class="form-actions">
        <button class="btn btn-secondary" onclick="prevStep(3)">السابق</button>
        <button class="btn btn-primary" onclick="nextStep(5)">التالي</button>
    </div>
        </div>

<!-- الخطوة 5: اختيار الألوان -->
<div class="form-step" id="step5">
    <div class="step-header">
        <h2>اختيار الألوان</h2>
    </div>

    <!-- الألوان الخارجية -->
    <div class="input-group">
            <label class="required">اللون الخارجي للمركبة</label>
    <small class="help-text">اختر اللون الخارجي للمركبة. يمكنك اختيار لون واحد أو لونين كحد أقصى.</small>
        <div class="color-options horizontal">
            <div class="color-option" style="background-color: #000000;" onclick="selectColor(this, 'external', 'أسود')">
                <span>أسود</span>
            </div>
            <div class="color-option" style="background-color: #FFFFFF;" onclick="selectColor(this, 'external', 'أبيض')">
                <span>أبيض</span>
            </div>
            <div class="color-option" style="background-color: #808080;" onclick="selectColor(this, 'external', 'رمادي')">
                <span>رمادي</span>
            </div>
            <div class="color-option" style="background-color: #FF0000;" onclick="selectColor(this, 'external', 'أحمر')">
                <span>أحمر</span>
            </div>
            <div class="color-option" style="background-color: #0000FF;" onclick="selectColor(this, 'external', 'أزرق')">
                <span>أزرق</span>
            </div>
            <div class="color-option" style="background-color: #008000;" onclick="selectColor(this, 'external', 'أخضر')">
                <span>أخضر</span>
            </div>
            <div class="color-option" style="background-color: #FFFF00;" onclick="selectColor(this, 'external', 'أصفر')">
                <span>أصفر</span>
            </div>
            <div class="color-option" style="background-color: #800080;" onclick="selectColor(this, 'external', 'بنفسجي')">
                <span>بنفسجي</span>
            </div>
            <div class="color-option" style="background-color: #FFA500;" onclick="selectColor(this, 'external', 'برتقالي')">
                <span>برتقالي</span>
            </div>
            <div class="color-option" style="background-color: #A52A2A;" onclick="selectColor(this, 'external', 'بني')">
                <span>بني</span>
            </div>
            <div class="color-option" style="background-color: #FFC0CB;" onclick="selectColor(this, 'external', 'وردي')">
                <span>وردي</span>
            </div>
            <div class="color-option" style="background-color: #00FFFF;" onclick="selectColor(this, 'external', 'سماوي')">
                <span>سماوي</span>
            </div>
            <div class="color-option" style="background-color: #FFD700;" onclick="selectColor(this, 'external', 'ذهبي')">
                <span>ذهبي</span>
            </div>
            <div class="color-option" style="background-color: #C0C0C0;" onclick="selectColor(this, 'external', 'فضي')">
                <span>فضي</span>
            </div>
            <div class="color-option" style="background-color: #964B00;" onclick="selectColor(this, 'external', 'برونزي')">
                <span>برونزي</span>
            </div>
        </div>
    </div>

    <!-- الألوان الداخلية -->
    <div class="input-group">
            <label class="required">اللون الداخلي للمركبة </label>
    <small class="help-text">اختر اللون الداخلي للمركبة. يمكنك اختيار لون واحد أو لونين كحد أقصى.</small>
        <div class="color-options horizontal">
            <div class="color-option" style="background-color: #000000;" onclick="selectColor(this, 'internal', 'أسود')">
                <span>أسود</span>
            </div>
            <div class="color-option" style="background-color: #FFFFFF;" onclick="selectColor(this, 'internal', 'أبيض')">
                <span>أبيض</span>
            </div>
            <div class="color-option" style="background-color: #808080;" onclick="selectColor(this, 'internal', 'رمادي')">
                <span>رمادي</span>
            </div>
            <div class="color-option" style="background-color: #FF0000;" onclick="selectColor(this, 'internal', 'أحمر')">
                <span>أحمر</span>
            </div>
            <div class="color-option" style="background-color: #0000FF;" onclick="selectColor(this, 'internal', 'أزرق')">
                <span>أزرق</span>
            </div>
            <div class="color-option" style="background-color: #008000;" onclick="selectColor(this, 'internal', 'أخضر')">
                <span>أخضر</span>
            </div>
            <div class="color-option" style="background-color: #FFFF00;" onclick="selectColor(this, 'internal', 'أصفر')">
                <span>أصفر</span>
            </div>
            <div class="color-option" style="background-color: #800080;" onclick="selectColor(this, 'internal', 'بنفسجي')">
                <span>بنفسجي</span>
            </div>
            <div class="color-option" style="background-color: #FFA500;" onclick="selectColor(this, 'internal', 'برتقالي')">
                <span>برتقالي</span>
            </div>
            <div class="color-option" style="background-color: #A52A2A;" onclick="selectColor(this, 'internal', 'بني')">
                <span>بني</span>
            </div>
            <div class="color-option" style="background-color: #FFC0CB;" onclick="selectColor(this, 'internal', 'وردي')">
                <span>وردي</span>
            </div>
            <div class="color-option" style="background-color: #00FFFF;" onclick="selectColor(this, 'internal', 'سماوي')">
                <span>سماوي</span>
            </div>
            <div class="color-option" style="background-color: #FFD700;" onclick="selectColor(this, 'internal', 'ذهبي')">
                <span>ذهبي</span>
            </div>
            <div class="color-option" style="background-color: #C0C0C0;" onclick="selectColor(this, 'internal', 'فضي')">
                <span>فضي</span>
            </div>
            <div class="color-option" style="background-color: #964B00;" onclick="selectColor(this, 'internal', 'برونزي')">
                <span>برونزي</span>
            </div>
        </div>
    </div>

    <!-- حالة الصبغ -->
    <div class="input-group" id="paintGroup">
        <label>حالة الصبغ</label>
        <div class="icon-options">
            <div class="icon-option" onclick="selectOption(this, 'paintCondition', 'صبغة الوكالة')">
                <i class="fa-solid fa-fill-drip"></i>
                <span>صبغة الوكالة</span>
            </div>
            <div class="icon-option" onclick="selectOption(this, 'paintCondition', 'مصبوغة')">
                <i class="fa-solid fa-spray-can"></i>
                <span>مصبوغة</span>
            </div>
            <div class="icon-option" onclick="selectOption(this, 'paintCondition', 'مصبوغة قليلاً')">
                <i class="fas fa-paint-brush"></i>
                <span>مصبوغة قليلاً</span>
            </div>
        </div>
        <small class="help-text">(اختياري)</small>
    </div>

    <div class="form-actions">
        <button class="btn btn-secondary" onclick="prevStep(4)">السابق</button>
        <button class="btn btn-primary" onclick="nextStep(6)">التالي</button>
    </div>
</div>
<!-- الخطوة 6: تحميل الصور -->
<!-- داخل قسم الخطوة 6 -->
<div class="form-step" id="step6">
    <div class="step-header">
        <h2>تحميل الصور</h2>
    </div>
<!-- مربع الصورة الرئيسية (مخفي في البداية) -->
<div id="mainImageBox" class="main-image-box hidden">
    <img id="mainImagePreview" src="" alt="الصورة الرئيسية">
</div>


<!-- زر تحميل الصور -->
<div class="upload-container">
    <div class="upload-box" onclick="document.getElementById('carImages').click()">
        <i class="fas fa-plus"></i>
        <p>انقر لإضافة الصور</p>
    </div>
</div>

<!-- شبكة عرض الصور المحملة -->
<div class="upload-grid" id="uploadGrid"></div>

<!-- حقل تحميل الصور المخفي -->
<input type="file" id="carImages" multiple hidden accept="image/*">

    <!-- ملاحظات مهمة -->
    <div class="review-card warning">
        <h3><i class="fas fa-exclamation-triangle"></i> ملاحظات مهمة</h3>
        <ul class="warning-list">
            <li>مسموح برفع 30 صورة + 1 فيديو فقط</li>
            <li>الصور يجب أن تكون واضحة وذات جودة عالية</li>
        </ul>
    </div>

    <!-- أزرار التنقل -->
    <div class="form-actions">
        <button class="btn btn-secondary" onclick="prevStep(5)">السابق</button>
        <button class="btn btn-primary" onclick="nextStep(7)">مراجعة الاعلان</button>
         <button class="btn btn-primary" onclick="nextStep(8)">نشر الاعلان</button>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/sortablejs@latest/Sortable.min.js"></script>

<style>
.review-card.warning {
    border-left: 4px solid #ffc107;
    background: #fff9e6;
}

.warning-list {
    list-style: none;
    padding: 0;
    color: #856404;
}

.warning-list li {
    padding: 5px 0;
    display: flex;
    align-items: center;
    gap: 8px;
}
</style>


<!-- الخطوة 7: مراجعة الإعلان -->
<div class="form-step" id="step7">
    <div class="step-header">
        <h2>مراجعة الإعلان</h2>
        <p>يرجى مراجعة المعلومات التالية قبل النشر:</p>
    </div>

    <div class="review-container">
        <!-- تفاصيل الإعلان -->
        <div class="review-card">
            <h3>تفاصيل الإعلان</h3>
            <div class="review-content">
                <div class="review-item">
                    <span class="review-label">نوع الإعلان:</span>
                    <span class="review-value" id="reviewAdType">غير محدد</span>
                </div>
                <div class="review-item">
                    <span class="review-label">نوع المركبة:</span>
                    <span class="review-value" id="reviewVehicleType">غير محدد</span>
                </div>
                <div class="review-item">
                    <span class="review-label">حالة المركبة:</span>
                    <span class="review-value" id="reviewVehicleCondition">غير محدد</span>
                </div>
                <div class="review-item">
                    <span class="review-label">العلامة التجارية:</span>
                    <span class="review-value" id="reviewBrand">غير محدد</span>
                </div>
                <div class="review-item">
                    <span class="review-label">الموديل:</span>
                    <span class="review-value" id="reviewModel">غير محدد</span>
                </div>
                <div class="review-item">
                    <span class="review-label">سنة الصنع:</span>
                    <span class="review-value" id="reviewYear">غير محدد</span>
                </div>
                <div class="review-item">
                    <span class="review-label">المسافة المقطوعة:</span>
                    <span class="review-value" id="reviewMileage">غير محدد</span>
                </div>
                <div class="review-item">
                    <span class="review-label">اللون الخارجي:</span>
                    <span class="review-value" id="reviewExternalColor">غير محدد</span>
                </div>
                <div class="review-item">
                    <span class="review-label">اللون الداخلي:</span>
                    <span class="review-value" id="reviewInternalColor">غير محدد</span>
                </div>
                <div class="review-item">
                    <span class="review-label">السعر المطلوب:</span>
                    <span class="review-value price">
                        <span id="reviewPrice">غير محدد</span>
                        <span class="currency">درهم</span>
</span>
</style>

<style>
.review-item .price {
    font-weight: 700;
    color: var(--primary-color);
    display: flex;
    align-items: center;
    gap: 5px;
}

.review-item .currency {
    font-size: 0.9em;
    color: #666;
}
</style>
                </div>
                <div class="review-item">
                    <span class="review-label">الوصف:</span>
                    <span class="review-value" id="reviewDescription">غير محدد</span>
                </div>
            </div>
        </div>
<button class="scroll-top-btn" onclick="window.scrollTo({top:0,behavior:'smooth'})">
    <i class="fas fa-arrow-up"></i>
</button>


<style>
.color-preview {
    display: flex;
    gap: 10px;
}

.color-preview .color {
    width: 25px;
    height: 25px;
    border-radius: 50%;
    border: 2px solid #fff;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.color-preview .color::after {
    content: attr(data-type);
    position: absolute;
    bottom: -20px;
    font-size: 0.7em;
    color: #666;
}
</style>
<style>
.scroll-top-btn {
    position: fixed;
    bottom: 20px;
    left: 20px;
    background: var(--primary-color);
    color: white;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: none;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    box-shadow: 0 4px 12px rgba(79,70,229,0.3);
}
</style>
        <!-- الصور المرفقة -->
        <div class="review-card">
            <h3>الصور المرفقة</h3>
            <div class="review-images" id="reviewImages">
                <!-- سيتم إضافة الصور هنا -->
            </div>
        </div>
    </div>

    <!-- ملاحظات مهمة -->
    <div class="review-card warning">
        <h3><i class="fas fa-exclamation-triangle"></i> ملاحظات مهمة</h3>
        <ul class="warning-list">
            <li>تأكد من صحة جميع المعلومات قبل النشر</li>
            <li>الإعلانات المخالفة ستتم إزالتها</li>
        </ul>
    </div>

    <!-- أزرار التنقل -->
    <div class="form-actions">
        <button class="btn btn-secondary" onclick="prevStep(6)">السابق</button>
        <button class="btn btn-primary" onclick="nextStep(8)">التالي</button>
    </div>
</div>

        <!-- الخطوة 8: اختيار الباقة -->
        <div class="form-step" id="step8">
            <div class="step-header">
                <h2>اختيار الباقة</h2>
            </div>

            <div class="icon-options" style="flex-direction: column; gap: 15px;">
                <!-- باقة دعم الموقع بكوب قهوة -->
                <div class="icon-option coffee-package" onclick="selectPackage('coffee')">
                    <div style="display: flex; justify-content: space-between; width: 100%;">
                        <div>
                            <img src="https://i.postimg.cc/mkLHGfnb/coffee-cup-16350828.png" alt="كوب قهوة" style="width: 24px; height: 24px;">
                            <h3 style="margin: 0; color: white;">☕ دعم الموقع بكوب قهوة</h3>
                            <small style="color: white;">عرض لمدة 7 أيام - مشاهدات محدودة</small>
                        </div>
                        <span style="color: white; font-weight: bold;">30 درهم</span>
                    </div>
                </div>

                <!-- باقة مجانية -->
                <div class="icon-option" onclick="selectPackage('normal')">
                    <div style="display: flex; justify-content: space-between; width: 100%;">
                        <div>
                            <img src="https://i.postimg.cc/4NFhj0Qg/free-15345505.png" alt="مجاني" style="width: 24px; height: 24px;">
                            <h3 style="margin: 0;">□ إعلان عادي مجاني</h3>
                            <small>عرض لمدة 7 أيام - مشاهدات محدودة</small>
                        </div>
                        <span style="color: var(--primary-color); font-weight: bold;">مجاني</span>
                    </div>
                </div>

                <!-- باقة توربو -->
                <div class="icon-option turbo" onclick="selectPackage('turbo')">
                    <div style="display: flex; justify-content: space-between; width: 100%;">
                        <div>
                            <img src="https://i.postimg.cc/mZj9ykch/3902021.png" alt="توربو" style="width: 24px; height: 24px;">
                            <h3 style="margin: 0;">★ اشتراك توربو المميز</h3>
                            <small>عرض لمدة شهر - مشاهدات 20x - عدد لا محدود من الإعلانات</small>
                        </div>
                        <span style="color: var(--primary-color); font-weight: bold;">129 درهم</span>
                    </div>
                </div>

                <!-- باقة VIP -->
                <div class="icon-option vip-package" onclick="selectPackage('vip')">
                    <div style="display: flex; justify-content: space-between; width: 100%;">
                        <div>
                            <img src="https://i.postimg.cc/285ZcYvG/eagle.png" alt="VIP" style="width: 24px; height: 24px;">
                            <h3 style="margin: 0;">🦅 باقة VIP الذهبية</h3>
                            <small>عرض لمدة 3 أشهر - مشاهدات 50x - أولوية في النتائج</small>
                        </div>
                        <span style="color: var(--gold-color); font-weight: bold;">259 درهم</span>
                    </div>
                </div>
            </div>

            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(7)">السابق</button>
                <button class="btn btn-primary" onclick="nextStep(9)">ارسال الإعلان</button>
            </div>
        </div>

        <!-- الخطوة 9: الدفع -->
        <div class="form-step hidden" id="step9">
            <div class="step-header">
                <h2>الدفع الإلكتروني</h2>
            </div>

            <!-- نموذج الدفع -->
            <div class="input-group">
                <label>رقم البطاقة</label>
                <div id="card-element" style="padding: 10px; border: 1px solid #ccc; border-radius: 8px;"></div>
            </div>

            <!-- رسائل الأخطاء -->
            <div id="card-errors" role="alert" style="color: #dc3545; margin-top: 10px;"></div>
<!-- حقل إدخال الكود -->
<div class="input-group">
    <label>أدخل كود الخصم (اختياري)</label>
    <div style="display: flex; gap: 10px; align-items: center;">
        <input type="text" id="discountCode" placeholder="أدخل كود الخصم" style="flex: 1; padding: 10px; border: 2px solid var(--border-color); border-radius: 8px;">
        <button class="btn btn-secondary" onclick="applyDiscount()">تطبيق الخصم</button>
    </div>
</div>

<!-- رسالة الخطأ أو النجاح -->
<div id="discountMessage" style="margin-top: 10px; font-size: 0.9rem; text-align: center;"></div>
<!-- الفاتورة -->
<div class="input-group">
    <label>الفاتورة</label>
    <div id="invoice" style="padding: 15px; border: 1px solid var(--border-color); border-radius: 8px;">
        <div class="invoice-item">
            <span>المبلغ المطلوب:</span>
            <span id="originalAmount">0 درهم</span>
        </div>
        <div class="invoice-item hidden" id="discountDetails">
            <div class="invoice-item">
                <span>الخصم (10%):</span>
                <span id="discountAmount">0 درهم</span>
            </div>
            <div class="invoice-item total">
                <span>المبلغ بعد الخصم:</span>
                <span id="finalAmount">0 درهم</span>
            </div>
            <div class="invoice-item saved">
                <span>المبلغ الذي وفرته:</span>
                <span id="savedAmount">0 درهم</span>
            </div>
        </div>
                </div>

        <div class="review-card warning">
    <h3><i class="fa-duotone fa-solid fa-check-to-slot" style="--fa-primary-color: #0ed82f; --fa-secondary-color: #0ed82f;"></i> دفع آمن بكل سهولة.</h3>
    <ul class="warning-list">
    </ul>
</div>

<style>
.review-card.warning {
    border-left: 4px solid #ffc107;
    background: #fff9e6;
}

.warning-list {
    list-style: none;
    padding: 0;
    color: #856404;
}

.warning-list li {
    padding: 5px 0;
    display: flex;
    align-items: center;
    gap: 8px;
}
</style>
            <div class="form-actions">
                <button class="btn btn-secondary" onclick="prevStep(8)">السابق</button>
                <button class="btn btn-primary" onclick="submitPayment()">اكتمال الدفع</button>
            </div>
        </div>
    </div>

    <script>
        // بيانات المركبات الكاملة
const vehicleData = {
    car: {
        brands: [
            "تويوتا", "فورد", "بي إم دبليو", "مرسيدس", "أودي", "هيونداي", "كيا", "نيسان", "شيفروليه", "فولكس فاجن",
            "هوندا", "مازدا", "ميتسوبيشي", "لكزس", "جيب", "رينو", "بيجو", "سكودا", "فيات", "سوزوكي",
            "فولفو", "سوبارو", "جاكوار", "لاند روفر", "تيسلا", "بورش", "ميني", "ألفا روميو", "فيراري", "لامبورغيني",
            "بنتلي", "رولز رويس", "أستون مارتن", "مكلارين", "بوجاتي", "كاديلاك", "لينكولن", "كرايسلر", "دودج", "رام",
            "جينيسيس", "إنفينيتي", "أكورا", "لوتس", "مازيراتي", "أوبل", "سيات", "داسيا", "سانج يونج", "بروتون",
            "تاتا", "ماهيندرا", "فاو", "جريت وول", "بي واي دي", "شيري", "جيلي", "هافال", "فينيكس", "زوتي",
            "فينفاست", "ليفان", "دونج فنغ", "بريليانس", "جاك", "روز رايز", "فوتون", "جاكوار لاند روفر", "سايك موتور", "كايمنز",
            "فورد موتور", "جنرال موتورز", "تويوتا موتور", "فولكس فاجن جروب", "هيونداي موتور", "نيسان موتور", "هوندا موتور", "بي إم دبليو جروب", "مرسيدس بنز", "فيات كرايسلر",
            "رينو جروب", "بي إس إيه جروب", "تيسلا موتورز", "فولفو كارز", "سوبارو", "مازدا موتور", "سوزوكي موتور", "ميتسوبيشي موتورز", "جيب", "لكزس",
            "أودي", "بورش", "ميني", "ألفا روميو", "فيراري", "لامبورغيني", "بنتلي", "رولز رويس", "أستون مارتن", "مكلارين",
            "بوجاتي", "كاديلاك", "لينكولن", "كرايسلر", "دودج", "رام", "جينيسيس", "إنفينيتي", "أكورا", "لوتس", "أخرى"
        ],
        models: {
            "تويوتا": ["كورولا", "كامري", "راف4", "لاند كروزر", "هايلكس", "برادو", "ياريس", "افينسيس", "سي-هير", "تندرا", "أخرى"],
            "فورد": ["فوكس", "موستانج", "إكسبلورر", "فوكس", "رينجر", "فوكس", "فيوجن", "إيدج", "إسكيب", "فليكس", "أخرى"],
            // ... (نفس القائمة السابقة لكل ماركة)
            "أخرى": ["أخرى"]
        },
        categories: ["سيدان", "SUV", "كوبيه", "هاتشباك", "بيك أب", "أخرى"]
    },
    motorcycle: {
        brands: [
            "هارلي ديفيدسون", "هوندا", "ياماها", "كاواساكي", "سوزوكي", "بي إم دبليو", "دوكاتي", "ك تي إم", "تريومف", "إنديان",
            "أخرى"
        ],
        models: {
            "هارلي ديفيدسون": ["سبورتستر", "فايت جلاد", "ستريت جلاد", "دينالي", "هيريتج كلاسيك", "أخرى"],
            "هوندا": ["CBR", "CB", "CRF", "GOLDWING", "AFRICA TWIN", "أخرى"],
            "ياماها": ["YZF-R1", "MT-07", "MT-09", "XTZ", "YZF-R6", "أخرى"],
            "كاواساكي": ["Ninja", "Z", "Vulcan", "Versys", "KLR", "أخرى"],
            "سوزوكي": ["GSX-R", "Hayabusa", "V-Strom", "Boulevard", "DR-Z", "أخرى"],
            "بي إم دبليو": ["R 1250 GS", "S 1000 RR", "F 750 GS", "R nineT", "K 1600", "أخرى"],
            "دوكاتي": ["Panigale", "Monster", "Multistrada", "Diavel", "Scrambler", "أخرى"],
            "ك تي إم": ["Duke", "RC", "Adventure", "Super Duke", "Enduro", "أخرى"],
            "تريومف": ["Bonneville", "Tiger", "Street Triple", "Rocket 3", "Speed Triple", "أخرى"],
            "إنديان": ["Scout", "Chief", "Chieftain", "Springfield", "FTR", "أخرى"],
            "أخرى": ["أخرى"]
        },
        categories: ["رياضية", "كلاسيكية", "مغامرات", "سكوتر", "أخرى"]
    },
    truck: {
        brands: [
            "فولفو", "مرسيدس", "مان", "سكانيا", "داف", "إيفيكو", "بيتربيلت", "كينوورث", "فريتلاينر", "هينو",
            "أخرى"
        ],
        models: {
            "فولفو": ["FH", "FM", "VNL", "VNR", "VNX", "أخرى"],
            "مرسيدس": ["Actros", "Arocs", "Antos", "Axor", "Econic", "أخرى"],
            "مان": ["TGX", "TGS", "TGM", "TGL", "TGE", "أخرى"],
            "سكانيا": ["R-series", "S-series", "G-series", "P-series", "L-series", "أخرى"],
            "داف": ["XF", "CF", "LF", "XF105", "CF85", "أخرى"],
            "إيفيكو": ["Stralis", "Trakker", "Daily", "Eurocargo", "S-Way", "أخرى"],
            "بيتربيلت": ["579", "389", "567", "520", "337", "أخرى"],
            "كينوورث": ["T680", "W900", "T880", "T800", "C500", "أخرى"],
            "فريتلاينر": ["Cascadia", "Coronado", "M2", "114SD", "122SD", "أخرى"],
            "هينو": ["500 Series", "700 Series", "300 Series", "600 Series", "800 Series", "أخرى"],
            "أخرى": ["أخرى"]
        },
        categories: ["شاحنة", "مقطورة", "نقل ثقيل", "نقل خفيف", "أخرى"]
    },
    boat: {
        brands: [
            "سي راي", "بايا لينر", "فيريتي", "برونسون", "فايكينغ", "أخرى"
        ],
        models: {
            "سي راي": ["240 Sundancer", "350 Express Cruiser", "510 Fly", "280 Bowrider", "310 Sun Sport", "أخرى"],
            "بايا لينر": ["VR5", "VR6", "VR7", "VR8", "VR9", "أخرى"],
            "فيريتي": ["V37", "V46", "V52", "V62", "V72", "أخرى"],
            "برونسون": ["Antares", "Barracuda", "Flyer", "Outremer", "Swift Trawler", "أخرى"],
            "فايكينغ": ["Sport Cruiser", "Open", "Coupé", "Flybridge", "Long Cabin", "أخرى"],
            "أخرى": ["أخرى"]
        },
        categories: ["يخت", "قارب صيد", "قارب شراعي", "قارب سريع", "أخرى"]
    }
};

// دالة لتحميل الماركات بناءً على نوع المركبة
function loadBrands(type) {
    const brands = vehicleData[type].brands || [];
    const brandSelect = document.getElementById('brandSelect');
    brandSelect.innerHTML = brands.map(brand => `<option>${brand}</option>`).join('');
}

function loadModels() {
    const brandSelect = document.getElementById('brandSelect');
    const modelSelect = document.getElementById('modelSelect');
    const selectedBrand = brandSelect.value;

    // مسح الموديلات القديمة
    modelSelect.innerHTML = '<option value="">اختر الموديل</option>';

    // تحميل الموديلات بناءً على نوع المركبة والعلامة التجارية
    if (selectedBrand && selectedVehicleType && vehicleData[selectedVehicleType].models[selectedBrand]) {
        vehicleData[selectedVehicleType].models[selectedBrand].forEach(model => {
            const option = document.createElement('option');
            option.value = model;
            option.textContent = model;
            modelSelect.appendChild(option);
        });
    }
}


        // بيانات الدول ورموزها
        const countryCodes1 = {
            'الإمارات': '+971',
            'السعودية': '+966',
            'عمان': '+968'
        };


        // بيانات الدول ورموزها
        const countryCodes = {
            'الإمارات': '+971',
            'السعودية': '+966',
            'عمان': '+968'
        };
        
        

// بيانات العملات
const currencies = {
    'الإمارات': 'AED', // الدرهم الإماراتي
    'السعودية': 'SAR', // الريال السعودي
    'عمان': 'OMR' // الريال العماني
};

        // بيانات المناطق لكل دولة
        const regions = {
            'الإمارات': ['دبي', 'أبوظبي', 'الشارقة', 'عجمان', 'رأس الخيمة', 'الفجيرة', 'أم القيوين', 'العين'],
            'السعودية': ['الرياض', 'جدة', 'مكة', 'المدينة', 'الدمام', 'الخبر'],
            'عمان': ['مسقط', 'صلالة', 'صحار', 'نزوى', 'صور']
        };

        // بيانات الأحياء لكل منطقة
        const neighborhoods = {
            'دبي': ['بر دبي', 'ديرة', 'جبل علي', 'المرقبات'],
            'أبوظبي': ['الشامخة', 'المرفأ', 'الخالدية', 'النهضة'],
            'الرياض': ['الملز', 'العليا', 'النخيل', 'الربيع'],
            'جدة': ['الصفا', 'الزهراء', 'الروضة', 'النسيم']
        };
let selectedRegions = []; // لتخزين المناطق المحددة
let selectedNeighborhoods = []; // لتخزين الأحياء المحددة
        let currentStep = 1;
let selectedProblems = []; // لتخزين المشكلات المحددة
        let selectedVehicleType = null;
        let selectedCountry = null;
        let selectedPackage = null;
        let adType = null;
        let adCategory = null;
        let paymentOptions = [];
        let selectedRegion = null;
        let selectedNeighborhood = null;
        let selectedExternalColors = [];
let selectedInternalColors = []; 
        let selectedExternalColor = null;
        let selectedInternalColor = null;
        let isNegotiable = false;
        let isUrgentSale = false;
        let selectedPlateType = null;
let selectedPlateCategory = null;
let selectedPlateRegistration = null;
let selectedPlateOwnership = null;
let selectedPaymentMethod = null;
let paymentMethods = [];
        let currentSubStep = null; // لتخزين الخطوة الثانوية الحالية
let mainImageBox = document.querySelector('.main-image-box');
let uploadGrid = document.getElementById('uploadGrid');
let carImagesInput = document.getElementById('carImages');

        // تهيئة Stripe
        const stripe = Stripe('pk_live_51QojAfI1bu8rsN6LBE4baN1wkoo7UoryVTgJ9uu9gixDmTM399NYsoNQZFTpa7umkCjNhuTBcGnBQ4Ry7Fm6nMrF00uSQjsWrx');
        const elements = stripe.elements();
        const cardElement = elements.create('card', {
            style: {
                base: {
                    fontSize: '16px',
                    color: '#32325d',
                    fontFamily: '"Tajawal", sans-serif',
                    '::placeholder': {
                        color: '#aab7c4'
                    }
                },
                invalid: {
                    color: '#dc3545'
                }
            }
        });

        // إضافة عنصر البطاقة إلى النموذج
        cardElement.mount('#card-element');

        // عرض أخطاء البطاقة
        cardElement.on('change', (event) => {
            const displayError = document.getElementById('card-errors');
            if (event.error) {
                displayError.textContent = event.error.message;
            } else {
                displayError.textContent = '';
            }
        });


        function selectCountry(country, element) {
            selectedCountry = country;
                selectedCountryCode = countryCodes[country]; // تحديث المتغير
                
            selectedCountry1 = country;
                selectedCountryCode1 = countryCodes1[country]; // تحديث المتغير
                
            document.querySelectorAll('.country-option').forEach(opt => opt.classList.remove('active'));
    document.querySelectorAll('.country-option').forEach(opt => opt.classList.remove('active'));
    element.classList.add('active');
    
  // تحديث رمز العملة
    updateCurrencySymbol();

            // تحديث قائمة المناطق بناءً على الدولة المحددة
            const regionOptions = document.querySelector('.region-options');
            regionOptions.innerHTML = regions[country].map(region => `
                <div class="region-option" onclick="selectRegion('${region}', this)">${region}</div>
            `).join('');
        }


// متغير لتخزين الصورة الرئيسية
let mainImageIndex = 0;
// عند تحميل الصور
document.getElementById('carImages').addEventListener('change', function (e) {
    const files = Array.from(e.target.files);
    const uploadGrid = document.getElementById('uploadGrid');
    const mainImageBox = document.getElementById('mainImageBox');

    // إظهار مربع الصورة الرئيسية إذا كان مخفيًا
    if (files.length > 0 && mainImageBox.classList.contains('hidden')) {
        mainImageBox.classList.remove('hidden');
    }

    // مسح الصور القديمة (اختياري)
    uploadGrid.innerHTML = '';

    // تحميل الصور وعرضها
    files.forEach((file, index) => {
        const reader = new FileReader();
        reader.onload = (e) => {
            const box = document.createElement('div');
            box.className = 'upload-box';
            box.innerHTML = `
                <img src="${e.target.result}" alt="صورة ${index + 1}">
                <div class="remove-btn" onclick="removeImage(this)">✕</div>
            `;
            uploadGrid.appendChild(box);

            // تعيين الصورة الأولى كصورة رئيسية
            if (index === 0) {
                updateMainImage(file);
            }
        };
        reader.readAsDataURL(file);
    });
});


function updateMainImage(imageSrc) {
    const mainImagePreview = document.getElementById('mainImagePreview');
    const placeholder = document.querySelector('.placeholder');

    if (imageSrc) {
        mainImagePreview.src = imageSrc;
        mainImagePreview.classList.remove('hidden');
        placeholder.style.display = 'none'; // إخفاء العنصر النائب
    } else {
        mainImagePreview.src = '';
        mainImagePreview.classList.add('hidden');
        placeholder.style.display = 'flex'; // إظهار العنصر النائب
    }
}


// دالة لتحديث الصورة الرئيسية
function updateMainImage(file) {
        const mainImagePreview = document.getElementById('mainImagePreview');
    const placeholder = document.querySelector('.placeholder');

    const reader = new FileReader();
    reader.onload = (e) => {
        document.getElementById('mainImagePreview').src = e.target.result;
    };
    reader.readAsDataURL(file);
}

// تمكين سحب الصور وإفلاتها في المربع الرئيسي
new Sortable(uploadGrid, {
    animation: 150,
    handle: '.upload-box',
    onEnd: function (evt) {
        const mainImageBox = document.getElementById('mainImageBox');
        if (evt.to === mainImageBox) {
            const draggedImage = evt.item.querySelector('img');
            if (draggedImage) {
                document.getElementById('mainImagePreview').src = draggedImage.src;
            }
        }
    }
});



        function selectRegion(region, element) {
            if (selectedRegion === region) {
                selectedRegion = null;
                element.classList.remove('active');
            } else if (!selectedRegion || selectedRegions.length < 2) {
                selectedRegion = region;
                document.querySelectorAll('.region-option').forEach(opt => opt.classList.remove('active'));
                element.classList.add('active');
            } else {
                alert('يمكنك اختيار منطقة واحدة.');
            }

            // تحديث قائمة الأحياء بناءً على المنطقة المحددة
            const neighborhoodOptions = document.querySelector('.neighborhood-options');
            if (neighborhoods[region]) {
                neighborhoodOptions.innerHTML = neighborhoods[region].map(neighborhood => `
                    <div class="neighborhood-option" onclick="selectNeighborhood('${neighborhood}', this)">${neighborhood}</div>
                `).join('');
            } else {
                neighborhoodOptions.innerHTML = '';
            }
        }

        function selectNeighborhood(neighborhood, element) {
            if (selectedNeighborhood === neighborhood) {
                selectedNeighborhood = null;
                element.classList.remove('active');
            } else if (!selectedNeighborhood || selectedNeighborhoods.length < 2) {
                selectedNeighborhood = neighborhood;
                document.querySelectorAll('.neighborhood-option').forEach(opt => opt.classList.remove('active'));
                element.classList.add('active');
            } else {
                alert('يمكنك اختيار حي واحد.');
            }
        }
// تحديث دالة selectVehicleType لإظهار الخطوة 2.4 عند اختيار لوحات المركبات
function selectVehicleType(type) {
    selectedVehicleType = type;
    document.querySelectorAll('.icon-option').forEach(opt => opt.classList.remove('active'));
    document.querySelector(`[data-type="${type}"]`).classList.add('active');

    if (type === 'motorcycle') {
        changeStep('2-1'); // إظهار خطوة اختيار نوع الدراجة
    } else if (type === 'truck') {
        changeStep('2-2'); // إظهار خطوة اختيار نوع المركبة الثقيلة
    } else if (type === 'services') {
        changeStep('2-3'); // عرض خطوة اختيار نوع الخدمة
    } else if (type === 'plates') {
        changeStep('2-4'); // عرض خطوة تفاصيل لوحات المركبات
    } else if (type === 'services' || type === 'plates' || type === 'other') {
        changeStep('3-special'); // الانتقال مباشرة إلى الخطوة الخاصة
    } else {
                loadDynamicContent(); // تحميل المحتوى الديناميكي للسيارات
        changeStep(3); // الانتقال إلى الخطوة 3 العادية
    }
}

        function selectBikeType(type) {
            selectedBikeType = type;
            document.querySelectorAll('#step2-1 .icon-option').forEach(opt => opt.classList.remove('active'));
            event.target.closest('.icon-option').classList.add('active');
            loadDynamicContent();
        }

        function selectHeavyVehicleType(type) {
            selectedHeavyVehicleType = type;
            document.querySelectorAll('#step2-2 .icon-option').forEach(opt => opt.classList.remove('active'));
            event.target.closest('.icon-option').classList.add('active');
            loadDynamicContent();
        }

        function selectServiceType(type) {
            selectedServiceType = type;
            document.querySelectorAll('#step2-3 .icon-option').forEach(opt => opt.classList.remove('active'));
            event.target.closest('.icon-option').classList.add('active');
        }


// دالة لتحديد نوع الإعلان
function selectAdType1(type, element) {
    const options = element.parentElement.querySelectorAll('.icon-option');
    
    // إذا كان الخيار محددًا مسبقًا، قم بإلغاء التحديد
    if (element.classList.contains('active')) {
        element.classList.remove('active');
        adType = null; // إعادة تعيين القيمة
    } else {
        // تحديد الخيار الجديد
        options.forEach(opt => opt.classList.remove('active'));
        element.classList.add('active');
        adType = type; // حفظ القيمة المحددة
    }
}
        function selectAdType(type, element) {
            adType = type;
            document.querySelectorAll('#step3 .icon-option').forEach(opt => opt.classList.remove('active'));
            element.classList.add('active');
             // التحقق من نوع الإعلان وإخفاء/إظهار زر "حادث/سكراب"
    const accidentOption = document.getElementById('accidentOption');
    if (type === 'إيجار') {
        accidentOption.style.display = 'none'; // إخفاء الزر
    } else {
        accidentOption.style.display = 'flex'; // إظهار الزر
    }
            toggleAdOptions();
        }
function toggleOption(element, option) {
    // تبديل حالة الخيار (تفعيل أو إلغاء تفعيل)
    element.classList.toggle('active');

    // حفظ الخيارات المحددة
    if (element.classList.contains('active')) {
        // إذا كان الخيار مفعلاً، أضفه إلى القائمة
        if (!selectedOptions.includes(option)) {
            selectedOptions.push(option);
        }
    } else {
        // إذا كان الخيار غير مفعّل، أزله من القائمة
        selectedOptions = selectedOptions.filter(opt => opt !== option);
    }

    // عرض الخيارات المحددة (اختياري)
    console.log('الخيارات المحددة:', selectedOptions)
    ;console.log('رمز الدولة المحدد:', selectedCountryCode);
}
       function selectOption(element, group, value) {
    const options = element.parentElement.querySelectorAll('.icon-option');
    
    // التحقق مما إذا كان الخيار المحدد هو نفسه الخيار المحدد مسبقًا
    if (element.classList.contains('active')) {
        // إلغاء التحديد
        element.classList.remove('active');
        value = null; // إعادة تعيين القيمة إلى null
    } else {
        // تحديد الخيار الجديد
        options.forEach(opt => opt.classList.remove('active'));
        element.classList.add('active');
    }
// حفظ القيمة المحددة
    switch (group) {
        case 'adCategory':
            adCategory = value;
            togglePartTypeGroup(); // إظهار/إخفاء حقل "هل القطعة أصلية أو تجارية؟"
            break;
        // باقي الحالات...
    }
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
        case 'transmission':
            transmission = value;
            break;
        case 'fuelType':
            fuelType = value;
            break;
        case 'driveSystem':
            driveSystem = value;
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
    const partTypeGroup = document.getElementById('partTypeGroup'); // المجموعة الجديدة

    if (adType === 'إيجار') {
        exportGroup.style.display = 'none';
        paintGroup.style.display = 'none';
        registrationGroup.style.display = 'none';
        priceGroup.style.display = 'none';
        paymentGroup.style.display = 'none';
        rentalPricesGroup.style.display = 'block';
        insurancePricesGroup.style.display = 'block';
        partTypeGroup.style.display = 'none'; // إخفاء عند اختيار الإيجار
    } else if (adType === 'بيع') {
        exportGroup.style.display = 'block';
        paintGroup.style.display = 'block';
        registrationGroup.style.display = 'block';
        priceGroup.style.display = 'block';
        paymentGroup.style.display = 'block';
        rentalPricesGroup.style.display = 'none';
        insurancePricesGroup.style.display = 'none';
    }

    // إظهار أو إخفاء "هل القطعة أصلية أم تجارية؟" بناءً على اختيار "قطع غيار" أو "اكسسوارات"
    if (adCategory === 'قطع غيار' || adCategory === 'اكسسوارات') {
        partTypeGroup.style.display = 'block'; // إظهار
    } else {
        partTypeGroup.style.display = 'none'; // إخفاء
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

        function toggleNegotiable(element) {
            isNegotiable = !isNegotiable;
            element.classList.toggle('active');
        }

        function toggleUrgentSale(element) {
            isUrgentSale = !isUrgentSale;
            element.classList.toggle('active');
        }

       function selectColor(element, type, color) {
    if (type === 'external') {
        // إذا كان اللون محددًا بالفعل، قم بإزالته
        if (selectedExternalColors.includes(color)) {
            selectedExternalColors = selectedExternalColors.filter(c => c !== color);
            element.classList.remove('active');
        } else if (selectedExternalColors.length < 2) { // السماح باختيار لونين كحد أقصى
            selectedExternalColors.push(color);
            element.classList.add('active');
        } else {
            alert('يمكنك اختيار لونين خارجيين كحد أقصى.');
        }
    } else if (type === 'internal') {
        // إذا كان اللون محددًا بالفعل، قم بإزالته
        if (selectedInternalColors.includes(color)) {
            selectedInternalColors = selectedInternalColors.filter(c => c !== color);
            element.classList.remove('active');
        } else if (selectedInternalColors.length < 2) { // السماح باختيار لونين كحد أقصى
            selectedInternalColors.push(color);
            element.classList.add('active');
        } else {
            alert('يمكنك اختيار لونين داخليين كحد أقصى.');
        }
    }

    // عرض الألوان المحددة (اختياري)
    console.log('الألوان الخارجية المحددة:', selectedExternalColors);
    console.log('الألوان الداخلية المحددة:', selectedInternalColors);
}
function loadDynamicContent() {
    const container = document.getElementById('dynamicContent');
    let data;

    if (selectedVehicleType === 'motorcycle') {
        data = vehicleData.motorcycle;
    } else if (selectedVehicleType === 'truck') {
        data = vehicleData.truck;
    } else if (selectedVehicleType === 'boat') {
        data = vehicleData.boat;
    } else {
        data = vehicleData.car; // البيانات الخاصة بالسيارات
    }

    // إنشاء الحقول الديناميكية
    container.innerHTML = `
        <div class="input-group">
            <label class="required">العلامة التجارية</label>
            <select id="brandSelect" onchange="loadModels()">
                ${data.brands.map(b => `<option>${b}</option>`).join('')}
            </select>
        </div>
        <div class="input-group">
            <label class="required">الموديل</label>
            <select id="modelSelect"></select>
        </div>
        <div class="input-group">
            <label class="required">الفئة</label>
            <select>${data.categories.map(c => `<option>${c}</option>`).join('')}</select>
        </div>
<div class="input-group">
    <label class="required">المسافة المقطوعة</label>
    <select id="mileage" required>
        <option value="" disabled selected>اختر المسافة المقطوعة</option>
        <option value="0-9999">0 إلى 9,999</option>
        <option value="10000-19999">10,000 إلى 19,999</option>
        <option value="20000-29999">20,000 إلى 29,999</option>
        <option value="30000-39999">30,000 إلى 39,999</option>
        <option value="40000-49999">40,000 إلى 49,999</option>
        <option value="50000-59999">50,000 إلى 59,999</option>
        <option value="60000-69999">60,000 إلى 69,999</option>
        <option value="70000-79999">70,000 إلى 79,999</option>
        <option value="80000-89999">80,000 إلى 89,999</option>
        <option value="90000-99999">90,000 إلى 99,999</option>
        <option value="100000-109999">100,000 إلى 109,999</option>
        <option value="110000-119999">110,000 إلى 119,999</option>
        <option value="120000-129999">120,000 إلى 129,999</option>
        <option value="130000-139999">130,000 إلى 139,999</option>
        <option value="140000-149999">140,000 إلى 149,999</option>
        <option value="150000-159999">150,000 إلى 159,999</option>
        <option value="160000-169999">160,000 إلى 169,999</option>
        <option value="170000-179999">170,000 إلى 179,999</option>
        <option value="180000-189999">180,000 إلى 189,999</option>
        <option value="190000-199999">190,000 إلى 199,999</option>
        <option value="200000+">أكثر من +200,000</option>
        <option value="300000+">أكثر من +300,000</option>
    </select>
        </div>
    `;

    // تحميل الموديلات بناءً على العلامة التجارية المحددة
    loadModels();
}

function toggleUnit() {
    const mileageInput = document.getElementById('mileage');
    const unitButton = document.querySelector('.btn-secondary');
    if (unitButton.textContent === 'كيلومتر/ميل') {
        mileageInput.placeholder = 'أدخل المسافة المقطوعة (ميل)';
        unitButton.textContent = 'ميل/كيلومتر';
    } else {
        mileageInput.placeholder = 'أدخل المسافة المقطوعة (كيلومتر)';
        unitButton.textContent = 'كيلومتر/ميل';
    }
}

function selectPackage(pkg) {
    selectedPackage = pkg;
    document.querySelectorAll('.icon-option').forEach(opt => opt.classList.remove('active'));
    event.target.closest('.icon-option').classList.add('active');

    // تحديث الفاتورة
    const originalAmountElement = document.getElementById('originalAmount');
    const discountDetails = document.getElementById('discountDetails');
    const discountMessage = document.getElementById('discountMessage');

    let originalAmount = 0;
    if (pkg === 'coffee') originalAmount = 30;
    else if (pkg === 'turbo') originalAmount = 129;
    else if (pkg === 'vip') originalAmount = 259;

    // تحديث المبلغ الأساسي
    originalAmountElement.textContent = `${originalAmount} درهم`;

    // إخفاء تفاصيل الخصم إذا كانت ظاهرة
    discountDetails.classList.add('hidden');
    discountMessage.textContent = '';
    discountMessage.classList.remove('error');

    // إعادة تعيين حالة الخصم
    isDiscountApplied = false;
}


function nextStep(step) {
    // التحقق من صحة الخطوة الحالية قبل الانتقال
    if (!validateStep(currentStep)) {
        return; // إذا لم تكن البيانات صحيحة، لا تنتقل إلى الخطوة التالية
    }

    // إذا كان الإعلان عن لوحات مركبات أو خدمات مركبات، تخطي خطوة تفاصيل الاتصال
    if (selectedVehicleType === 'plates' || selectedVehicleType === 'services') {
        if (step === 4) { // خطوة تفاصيل الاتصال
            step = 6; // الانتقال مباشرة إلى الخطوة 6 (تحميل الصور)
        }
    }

    // إذا كانت الخطوة 7 (مراجعة الإعلان)، قم بتحديث بيانات المراجعة
    if (step === 7) {
        updateReviewStep(); // تحديث بيانات المراجعة قبل الانتقال إلى الخطوة 7
    }

    // إذا كانت الخطوة 9 (الدفع)، قم بالتحقق من الباقة المحددة
    if (step === 9) {
        if (selectedPackage === 'turbo' || selectedPackage === 'vip' || selectedPackage === 'coffee') {
            changeStep(9); // الانتقال إلى الدفع
        } else {
            submitForm(); // إرسال الإعلان مباشرة للباقة المجانية
        }
        return;
    }

    // تغيير الخطوة في الحالات العادية
    changeStep(step);
}

function changeMainImage() {
    const mainImageBox = document.getElementById('mainImageBox');
    const uploadGrid = document.getElementById('uploadGrid');
    const images = uploadGrid.querySelectorAll('.upload-box img');
    if (images.length > 0) {
        const newMainImage = images[0].src; // اختيار الصورة الأولى كصورة رئيسية
        document.getElementById('mainImagePreview').src = newMainImage;
    } else {
        alert('لا توجد صور متاحة لتغيير الصورة الرئيسية.');
    }
}


mainImageBox.addEventListener('dragover', (e) => {
    e.preventDefault();
    mainImageBox.style.border = '3px dashed var(--primary-color)';
});

mainImageBox.addEventListener('dragleave', () => {
    mainImageBox.style.border = '3px dashed var(--border-color)';
});

mainImageBox.addEventListener('drop', (e) => {
    e.preventDefault();
    mainImageBox.style.border = '3px dashed var(--border-color)';

    // الحصول على الصورة المسحوبة
    const draggedImage = e.dataTransfer.getData('text/plain');
    if (draggedImage) {
        updateMainImage(draggedImage); // تحديث الصورة الرئيسية
    } else {
        alert('يرجى سحب صورة صالحة.');
    }
});




        function changeStep(step) {
    // إخفاء جميع الخطوات
    document.querySelectorAll('.form-step').forEach(s => s.classList.remove('active'));

    if (step === 4) {
        // تحديث رمز الدولة في الخطوة 4
        document.getElementById('countryCode').value = selectedCountryCode;
    }
        // تحديث رمز الدولة في الخطوات الخاصة
    if (step === '2-3') { // خدمات المركبات
        document.getElementById('countryCodeServices').value = selectedCountryCode;
    } else if (step === '2-4') { // لوحات المركبات
        document.getElementById('countryCodePlates').value = selectedCountryCode;
    } else if (step === '3-special') { // إعلانات مبوبة أخرى
        document.getElementById('countryCodeSpecial').value = selectedCountryCode;
    }
        // إذا كان النوع من الأنواع الخاصة (لوحات مركبات أو خدمات مركبات)، نتأكد من عدم عرض الخطوات 3 و 4 و 5
    if (selectedVehicleType === 'plates' || selectedVehicleType === 'services') {
        if (step === 3 || step === 4 || step === 5) {
            step = 6; // الانتقال مباشرة إلى الخطوة 6 (تحميل الصور)
        }
    }

    // عرض الخطوة المطلوبة
    document.getElementById(`step${step}`).classList.add('active');
    currentStep = step;
    updateProgress();
}

    function updateProgress() {
    const steps = document.querySelectorAll('.step-circle');
    steps.forEach((circle, index) => {
                // إخفاء الخطوات 3 و 4 و 5 عند اختيار الأنواع الخاصة
        if (selectedVehicleType === 'plates' || selectedVehicleType === 'services') {
            if (index === 2 || index === 3 || index === 4) { // الخطوات 3 و 4 و 5
                circle.classList.add('hidden');
            } else {
                circle.classList.remove('hidden');
            }
        } else {
            // إظهار جميع الخطوات عند اختيار الأنواع العادية
            circle.classList.remove('hidden');
        }

        // تحديث حالة الخطوات (تفعيل أو إلغاء تفعيل)
        circle.classList.toggle('active', index < currentStep);
    });

    // إخفاء الخطوة 9 إلا عند اختيار الباقات المدفوعة
    const step9 = document.querySelector('.step-circle[onclick="changeStep(9)"]');
    if (selectedPackage === 'turbo' || selectedPackage === 'vip' || selectedPackage === 'coffee') {
        step9.classList.remove('hidden');
    } else {
        step9.classList.add('hidden');
    }
}
// دالة للتحقق من صحة البيانات في الخطوة 2.4
function validateStep2_4() {
    if (!selectedPlateType || !selectedPlateCategory || !selectedPlateRegistration || !selectedPlateOwnership || !document.getElementById('plateDetails').value) {
        alert('يرجى ملء جميع الحقول المطلوبة');
        return false;
    }
    return true;
}


// دالة لإزالة الصورة
function removeImage(element) {
    const box = element.parentElement;
    box.remove();

    // إذا كانت الصورة المحذوفة هي الرئيسية، قم بتمييز الصورة التالية
    if (box.querySelector('img').src === document.getElementById('mainImagePreview').src) {
        const firstBox = document.querySelector('.upload-box');
        if (firstBox) {
            updateMainImage(firstBox.querySelector('img').src);
        } else {
            document.getElementById('mainImageBox').classList.add('hidden');
        }
    }
}


function handleImageUpload(files) {
    const uploadGrid = document.getElementById('uploadGrid');
    const mainImageBox = document.getElementById('mainImageBox');

    // إظهار مربع الصورة الرئيسية إذا كان مخفيًا
    if (files.length > 0 && mainImageBox.classList.contains('hidden')) {
        mainImageBox.classList.remove('hidden');
    }

    // مسح الصور القديمة (اختياري)
    uploadGrid.innerHTML = '';

    // تحميل الصور وعرضها
    files.forEach((file, index) => {
        const reader = new FileReader();
        reader.onload = (e) => {
            const box = document.createElement('div');
            box.className = 'upload-box';
            box.innerHTML = `
                <img src="${e.target.result}" alt="صورة ${index + 1}">
                <div class="remove-btn" onclick="removeImage(this)">✕</div>
            `;
            uploadGrid.appendChild(box);

            // تعيين الصورة الأولى كصورة رئيسية
            if (index === 0) {
                updateMainImage(file);
            }
        };
        reader.readAsDataURL(file);
    });
}

     
 // تهيئة Sortable.js لسحب وإفلات الصور// تهيئة Sortable.js لسحب وإفلات الصور
new Sortable(uploadGrid, {
    animation: 150,
    handle: '.upload-box',
    onEnd: function (evt) {
        if (evt.to === mainImageBox) {
            const draggedImage = evt.item.querySelector('img');
            if (draggedImage) {
                updateMainImage(draggedImage.src); // تحديث الصورة الرئيسية
            }
        }
    }
});


uploadGrid.addEventListener('dragstart', (e) => {
    if (e.target.tagName === 'IMG') {
        e.dataTransfer.setData('text/plain', e.target.src); // إرسال مصدر الصورة
    }
});


// دالة لتحديث الصورة الرئيسية عند السحب والإفلات
function updateMainImage() {
    const firstImage = uploadGrid.querySelector('.upload-box img');
    if (firstImage) {
        mainImageBox.innerHTML = `
            <img src="${firstImage.src}" alt="الصورة الرئيسية">
            <div class="remove-btn" onclick="removeMainImage()">✕</div>
        `;
    }
}
        async function submitPayment() {
            const { paymentMethod, error } = await stripe.createPaymentMethod({
                type: 'card',
                card: cardElement,
            });
            
            
            function setMainImage(index) {
    const images = document.querySelectorAll('.upload-box img');
    images.forEach((img, i) => {
        if (i === index) {
            img.parentElement.classList.add('main-image-indicator');
        } else {
            img.parentElement.classList.remove('main-image-indicator');
        }
    });
}
            
            
function removeMainImage() {
    const mainImagePreview = document.getElementById('mainImagePreview');
    mainImagePreview.src = '';
    mainImagePreview.classList.add('hidden');
    document.querySelector('.placeholder').style.display = 'flex';
}
            if (error) {
                // عرض رسالة الخطأ
                const displayError = document.getElementById('card-errors');
                displayError.textContent = error.message;
            } else {
                // إرسال paymentMethod.id إلى الخادم لمعالجة الدفع
                fetch('/your-server-endpoint', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({ paymentMethodId: paymentMethod.id }),
                })
                .then(response => response.json())
                .then(data => {
                    if (data.success) {
                        alert('تمت عملية الدفع بنجاح!');
                        submitForm(); // إكمال الإعلان
                    } else {
                        alert('فشلت عملية الدفع. يرجى المحاولة مرة أخرى.');
                    }
                })
                .catch(error => {
                    console.error('Error:', error);
                    alert('حدث خطأ أثناء معالجة الدفع.');
                });
            }
        }


function validateStep(step) {
    let isValid = true;

    if (step === 1) {
        if (!selectedCountry || !selectedRegion) {
            isValid = false;
            alert('يرجى اختيار الدولة والمنطقة');
        }
    } else if (step === 3) {
        if (!adType || !adCategory) {
            isValid = false;
            alert('يرجى اختيار جميع الخيارات المطلوبة');
        }
    } else if (step === 5) {
        // التحقق من اختيار الألوان الخارجية والداخلية
        if (selectedExternalColors.length === 0 || selectedInternalColors.length === 0) {
            isValid = false;
            alert('يرجى اختيار الألوان الخارجية والداخلية');
        }
    }

    return isValid;
}
        function submitForm() {
            if (validateStep(currentStep)) {
                alert('تم إرسال الإعلان بنجاح!');
                document.querySelectorAll('.form-step').forEach(s => s.classList.remove('active'));
                document.getElementById('step1').classList.add('active');
                currentStep = 1;
                updateProgress();
                resetForm();
            }
            
     }
    

// دالة لتمكين سحب وإفلات الصور
function sortableGrid() {
    const uploadGrid = document.querySelector('.upload-grid');
    new Sortable(uploadGrid, {
        animation: 150,
        handle: '.upload-box',
        onEnd: function (evt) {
            console.log('تم إعادة ترتيب الصور');
        }
    });
}
// دالة لتحديد نوع اللوحة
function selectPlateType(type, element) {
    selectedPlateType = type;
    const options = element.parentElement.querySelectorAll('.icon-option');
    options.forEach(opt => opt.classList.remove('active'));
    element.classList.add('active');
}
// دالة لتحديد فئة اللوحة (خصوصي أو كلاسيكي)
function selectPlateCategory(category, element) {
    selectedPlateCategory = category;
    const options = element.parentElement.querySelectorAll('.icon-option');
    options.forEach(opt => opt.classList.remove('active'));
    element.classList.add('active');
}

// دالة لتحديد حالة تسجيل اللوحة
function selectPlateRegistration(status, element) {
    selectedPlateRegistration = status;
    const options = element.parentElement.querySelectorAll('.icon-option');
    options.forEach(opt => opt.classList.remove('active'));
    element.classList.add('active');
}
// دالة لتحديث الحقول بناءً على نوع الإعلان
function updateAdditionalDetails() {
    const saleDetails = document.getElementById('saleDetails');
    const rentalDetails = document.getElementById('rentalDetails');

    if (adType === 'بيع') {
        saleDetails.classList.remove('hidden');
        rentalDetails.classList.add('hidden');
    } else if (adType === 'إيجار') {
        saleDetails.classList.add('hidden');
        rentalDetails.classList.remove('hidden');
    }
}

// دالة لتحديد طريقة الدفع
function selectPaymentMethod(method, element) {
    const options = element.parentElement.querySelectorAll('.icon-option');
    options.forEach(opt => opt.classList.remove('active'));
    element.classList.add('active');
    paymentMethod = method;
}



// دالة لتحديث الخطوة 4 عند تغيير الخطوة 3
function toggleAdOptions() {
    updateAdditionalDetails();
}


// دالة لتحديد ملكية اللوحة
function selectPlateOwnership(ownership, element) {
    selectedPlateOwnership = ownership;
    const options = element.parentElement.querySelectorAll('.icon-option');
    options.forEach(opt => opt.classList.remove('active'));
    element.classList.add('active');
}

function togglePaymentMethod(method, element) {
    element.classList.toggle('active');
    if (paymentMethods.includes(method)) {
        paymentMethods = paymentMethods.filter(m => m !== method);
    } else {
        paymentMethods.push(method);
    }
    console.log('طرق الدفع المحددة:', paymentMethods);
}
// دالة لتحديث رمز العملة بناءً على الدولة المحددة
function updateCurrencySymbol() {
    const currency = selectedCountry && currencies[selectedCountry] ? currencies[selectedCountry] : 'AED'; // افتراضي: AED


    // تحديث رمز العملة في الخطوة 3-special
    const currencySymbolSpecial = document.getElementById('currencySymbolSpecial');
    if (currencySymbolSpecial) {
        currencySymbolSpecial.textContent = currency;
    }
    

    // تحديث رمز العملة في قسم البيع
    const saleCurrencySymbol = document.getElementById('saleCurrencySymbol');
    if (saleCurrencySymbol) {
        saleCurrencySymbol.textContent = currency;
    }

    // تحديث رمز العملة في قسم الإيجار
    const rentalCurrencySymbols = document.querySelectorAll('.rentalCurrencySymbol');
    rentalCurrencySymbols.forEach(symbol => {
        symbol.textContent = currency;
    });
}

function togglePartTypeGroup() {
    const partTypeGroup = document.getElementById('partTypeGroup');
    if (adCategory === 'قطع غيار' || adCategory === 'اكسسوارات') {
        partTypeGroup.style.display = 'block'; // إظهار الحقل
    } else {
        partTypeGroup.style.display = 'none'; // إخفاء الحقل
    }
}
function selectPaymentMethod(method, element) {
    const options = element.parentElement.querySelectorAll('.icon-option');
    options.forEach(opt => opt.classList.remove('active'));
    element.classList.add('active');
    selectedPaymentMethod = method;
}
function updateReviewStep() {
    // تحديث نوع الإعلان
    document.getElementById('reviewAdType').textContent = adType || 'غير محدد';

    // تحديث المسافة المقطوعة
    const mileageSelect = document.getElementById('mileage');
    document.getElementById('reviewMileage').textContent = mileageSelect ? mileageSelect.options[mileageSelect.selectedIndex].text : 'غير محدد';

    // تحديث نوع المركبة
    document.getElementById('reviewVehicleType').textContent = selectedVehicleType || 'غير محدد';

    // تحديث حالة المركبة
    document.getElementById('reviewVehicleCondition').textContent = vehicleCondition || 'غير محدد';

    // تحديث العلامة التجارية
    const brandSelect = document.getElementById('brandSelect');
    document.getElementById('reviewBrand').textContent = brandSelect ? brandSelect.value : 'غير محدد';

    // تحديث الموديل
    const modelSelect = document.getElementById('modelSelect');
    document.getElementById('reviewModel').textContent = modelSelect ? modelSelect.value : 'غير محدد';

    // تحديث سنة الصنع
    const yearSelect = document.getElementById('yearSelect');
    document.getElementById('reviewYear').textContent = yearSelect ? yearSelect.value : 'غير محدد';

    // تحديث المسافة المقطوعة
    const mileageInput = document.getElementById('mileage');
    document.getElementById('reviewMileage').textContent = mileageInput ? mileageInput.value + ' كم' : 'غير محدد';
 // عرض الألوان الخارجية
    const externalColorsDiv = document.getElementById('reviewExternalColor');
    externalColorsDiv.innerHTML = selectedExternalColors.map(color => `
        <div class="color-circle" style="background-color: ${getColorCode(color)};">
            <span>${color}</span>
        </div>
    `).join('');

    // عرض الألوان الداخلية
    const internalColorsDiv = document.getElementById('reviewInternalColor');
    internalColorsDiv.innerHTML = selectedInternalColors.map(color => `
        <div class="color-circle" style="background-color: ${getColorCode(color)};">
            <span>${color}</span>
        </div>
    `).join('');

    // تحديث السعر
    const priceInput = document.getElementById('price');
    document.getElementById('reviewPrice').textContent = priceInput ? priceInput.value + ' ' + (currencies[selectedCountry] || 'درهم') : 'غير محدد';

    // تحديث الوصف
    const descriptionInput = document.getElementById('description');
    document.getElementById('reviewDescription').textContent = descriptionInput ? descriptionInput.value : 'غير محدد';

    // تحديث الصور
    const reviewImages = document.getElementById('reviewImages');
    reviewImages.innerHTML = '';
    Array.from(document.querySelectorAll('.upload-box img')).forEach(img => {
        const imgElement = document.createElement('img');
        imgElement.src = img.src;
        reviewImages.appendChild(imgElement);
    });
}

// دالة للحصول على كود اللون بناءً على اسم اللون
function getColorCode(colorName) {
    const colorMap = {
        'أسود': '#000000',
        'أبيض': '#FFFFFF',
        'رمادي': '#808080',
        'أحمر': '#FF0000',
        'أزرق': '#0000FF',
        'أخضر': '#008000',
        'أصفر': '#FFFF00',
        'بنفسجي': '#800080',
        'برتقالي': '#FFA500',
        'بني': '#A52A2A',
        'وردي': '#FFC0CB',
        'سماوي': '#00FFFF',
        'ذهبي': '#FFD700',
        'فضي': '#C0C0C0',
        'برونزي': '#964B00'
    };
    return colorMap[colorName] || '#CCCCCC'; // لون افتراضي إذا لم يتم العثور على اللون
}
function selectProblem(problem, element) {
    // إلغاء تحديد جميع الخيارات
    document.querySelectorAll('#step4 .icon-option').forEach(opt => opt.classList.remove('active'));
    
    // تحديد الخيار الجديد
    element.classList.add('active');
    selectedProblem = problem;
    
    // عرض القيمة المحددة (اختياري)
    console.log('المشكلة المحددة:', selectedProblem);
}
function toggleProblem(problem, element) {
    // إذا كان الخيار محددًا بالفعل، قم بإزالته
    if (selectedProblems.includes(problem)) {
        selectedProblems = selectedProblems.filter(p => p !== problem);
        element.classList.remove('active');
    } else {
        // إذا كان الخيار غير محدد، قم بإضافته
        selectedProblems.push(problem);
        element.classList.add('active');
    }

    // عرض القيم المحددة (اختياري)
    console.log('المشكلات المحددة:', selectedProblems);
}

function prevStep() {
    // تحديد الخطوة السابقة بناءً على الخطوة الحالية
    let previousStep = currentStep - 1;

    // إذا كانت الخطوة الحالية هي الخطوة 6 (تحميل الصور) وكان النوع من الأنواع الخاصة (لوحات مركبات أو خدمات مركبات)
    if (currentStep === 6 && (selectedVehicleType === 'plates' || selectedVehicleType === 'services')) {
        previousStep = 2; // العودة إلى الخطوة 2 مباشرة
    }
    // إذا كانت الخطوة الحالية هي الخطوة 3-special (إعلانات مبوبة أخرى)
    else if (currentStep === '3-special') {
        previousStep = 2; // العودة إلى الخطوة 2
    }
    // إذا كانت الخطوة الحالية هي الخطوة 2-1 (اختيار نوع الدراجة)
    else if (currentStep === '2-1') {
        previousStep = 2; // العودة إلى الخطوة 2
    }
    // إذا كانت الخطوة الحالية هي الخطوة 2-2 (اختيار نوع المركبة الثقيلة)
    else if (currentStep === '2-2') {
        previousStep = 2; // العودة إلى الخطوة 2
    }
    // إذا كانت الخطوة الحالية هي الخطوة 2-3 (اختيار نوع الخدمة)
    else if (currentStep === '2-3') {
        previousStep = 2; // العودة إلى الخطوة 2
    }
    // إذا كانت الخطوة الحالية هي الخطوة 2-4 (تفاصيل لوحات المركبات)
    else if (currentStep === '2-4') {
        previousStep = 2; // العودة إلى الخطوة 2
    }
    // إذا كانت الخطوة الحالية هي الخطوة 1 (اختيار الدولة)
    else if (currentStep === 1) {
        alert('أنت بالفعل في الخطوة الأولى');
        return; // لا تفعل شيئًا إذا كان المستخدم في الخطوة الأولى
    }

    // تغيير الخطوة إلى الخطوة السابقة
    changeStep(previousStep);
}

// قائمة الأكواد الصالحة
const validDiscountCodes = ["HH127", "HH128", "HH129", "HH122", "HH121", "HH156", "HH153", "HH159", "HH158", "HH154"];

// متغير لتخزين حالة الخصم
let isDiscountApplied = false;
// دالة لتطبيق الخصم
function applyDiscount() {
    const discountCode = document.getElementById('discountCode').value.trim().toUpperCase();
    const discountMessage = document.getElementById('discountMessage');
    const originalAmountElement = document.getElementById('originalAmount');
    const discountAmountElement = document.getElementById('discountAmount');
    const finalAmountElement = document.getElementById('finalAmount');
    const savedAmountElement = document.getElementById('savedAmount');
    const discountDetails = document.getElementById('discountDetails');

    // التحقق من صحة الكود
    if (validDiscountCodes.includes(discountCode)) {
        if (!isDiscountApplied) {
            // تطبيق الخصم 10% على الباقات المدفوعة
            if (selectedPackage === 'coffee' || selectedPackage === 'turbo' || selectedPackage === 'vip') {
                let originalAmount = 0;
                if (selectedPackage === 'coffee') originalAmount = 30;
                else if (selectedPackage === 'turbo') originalAmount = 129;
                else if (selectedPackage === 'vip') originalAmount = 259;

                const discountAmount = originalAmount * 0.1; // خصم 10%
                const finalAmount = originalAmount - discountAmount; // المبلغ النهائي

                // تحديث الفاتورة
                originalAmountElement.textContent = `${originalAmount} درهم`;
                discountAmountElement.textContent = `-${discountAmount.toFixed(0)} درهم`;
                finalAmountElement.textContent = `${finalAmount.toFixed(0)} درهم`;
                savedAmountElement.textContent = `${discountAmount.toFixed(0)} درهم`;

                // إظهار تفاصيل الخصم
                discountDetails.classList.remove('hidden');

                discountMessage.textContent = 'تم تطبيق الخصم بنجاح!';
                discountMessage.classList.remove('error');
                isDiscountApplied = true;
            } else {
                discountMessage.textContent = 'الخصم متاح فقط للباقات المدفوعة.';
                discountMessage.classList.add('error');
            }
        } else {
            discountMessage.textContent = 'تم تطبيق الخصم مسبقًا.';
            discountMessage.classList.add('error');
        }
    } else {
        discountMessage.textContent = 'كود الخصم غير صحيح.';
        discountMessage.classList.add('error');
    }
}
        function resetForm() {
            document.querySelectorAll('input, select, textarea').forEach(element => {
                if (element.type !== 'button') {
                    element.value = '';
                }
            });
            document.querySelectorAll('.icon-option, .country-option, .region-option, .neighborhood-option').forEach(opt => {
                opt.classList.remove('active');
            });
            document.getElementById('previewContainer').innerHTML = '';
            selectedVehicleType = null;
            selectedCountry = null;
            selectedPackage = null;
            adType = null;
            adCategory = null;
            paymentOptions = [];
            selectedRegion = null;
            selectedNeighborhood = null;
            selectedExternalColor = null;
            selectedInternalColor = null;
            isNegotiable = false;
            isUrgentSale = false;
        }
    </script>
</body>
</html>
