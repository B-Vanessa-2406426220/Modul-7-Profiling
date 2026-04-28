# Performance Testing Result

## Before Optimization

### Test Plan 1: /all-student-request
- View Result Tree
  ![all-student-request_view-result-tree](assets/all-student-request/1-1.png)
- View Results in Table
  ![all-student-request_view-result-in-table](assets/all-student-request/1-2.png)
- Summary Report
  ![all-student-request_summary-report](assets/all-student-request/1-3.png)
- Graph Results
  ![all-student-request_graph-results](assets/all-student-request/1-4.png)

### Test Plan 2: /all-student-name
- View Result Tree
  ![all-student-name_view-result-tree](assets/all-student-name/2-1.png)
- View Results in Table
  ![all-student-name_view-results-in-table](assets/all-student-name/2-2.png)
- Summary Report
  ![all-student-name_summary-report](assets/all-student-name/2-3.png)
- Graph Results
  ![all-student-name_graph-results](assets/all-student-name/2-4.png)

### Test Plan 3: /highest-gpa
- View Result Tree
  ![highest-gpa_view-result-tree](assets/highest-gpa/3-1.png)
- View Results in Table
  ![highest-gpa_view-results-in-table](assets/highest-gpa/3-2.png)
- Summary Report
  ![highest-gpa_summary-report](assets/highest-gpa/3-3.png)
- Graph Results
  ![highest-gpa_graph-results](assets/highest-gpa/3-4.png)

Using Command Line:
/all-student-request
![/all-students-request_cli](assets/all-student-request/1-results.png)

/all-student-name
![/all-student-name_cli](assets/all-student-name/2-results.png)

/highest-gpa 
![/highest-gpa_cli](assets/highest-gpa/3-results.png)

## After Optimization
/all-student-request after
![/all-students-request_after](assets/all-student-request/1-2_after.png)

/all-student-name after
![/all-student-name_after](assets/all-student-name/2-2_after.png)

/highest-gpa after
![/highest-gpa_after](assets/highest-gpa/3-2_after.png)

## Profiling
/all-student-request after
![/all-students-request_improvement](assets/all-student-request/1-improvement.png)

/all-student-name after
![/all-student-name_improvement](assets/all-student-name/2-improvement.png)

/highest-gpa after
![/highest-gpa_improvement](assets/highest-gpa/3-improvement.png)

## Conclusion
Secara keseluruhan, hasil optimasi yang dilakukan menunjukkan peningkatan performa yang signifikan dan konsisten, baik dari sisi pengukuran JMeter maupun IntelliJ Profiler. Pada endpoint /all-student, refactoring method getAllStudentsWithCourses() dari pendekatan nested loop dengan N+1 query menjadi studentCourseRepository.findAll() berhasil menurunkan CPU time sebesar 74.0% (dari 5.644 ms menjadi 1.467 ms) berdasarkan profiling, dan rata-rata sample time JMeter turun drastis dari 63.322 ms menjadi 4.765 ms. Pada endpoint /all-student-name, perubahan method joinStudentNames() dari konkatenasi string dalam loop menjadi stream().map().collect(Collectors.joining()) menghasilkan penurunan CPU time sebesar 64.5% (dari 513 ms menjadi 182 ms) pada profiling, dan hasil JMeter pun mengkonfirmasi peningkatan yang besar dengan sample time turun dari 1.480 ms menjadi 88 ms. Pada endpoint /highest-gpa, penggantian loop manual dengan stream().max() memberikan peningkatan CPU time sebesar 25.7% (dari 280 ms menjadi 208 ms) dan sample time JMeter turun dari 139 ms menjadi 74 ms. Kesimpulannya, ketiga optimasi yang dilakukan terbukti efektif dan hasil JMeter sepenuhnya sejalan dengan temuan profiling, mengkonfirmasi bahwa eliminasi N+1 query dan penggunaan stream API memberikan dampak nyata terhadap performa aplikasi secara end-to-end.
