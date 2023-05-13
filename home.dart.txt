import 'package:flutter/material.dart';
import 'package:myapp/contact.dart';

class HomeView extends StatefulWidget {
  const HomeView({super.key});

  @override
  State<HomeView> createState() => _HomeViewState();
}

class _HomeViewState extends State<HomeView> {
  TextEditingController nameController = TextEditingController();
  TextEditingController numbController = TextEditingController();

  addContact() {
    setState(() {
      Contact.myContactList
          .add({"name": nameController.text, "number": numbController.text});
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButton: FloatingActionButton.extended(
          backgroundColor: Colors.teal,
          onPressed: () {
            showDialog(
                context: context,
                builder: (context) {
                  return Container(
                    child: AlertDialog(
                      title: const Text(
                        "Create new contact",
                        style: TextStyle(fontSize: 20),
                      ),
                      content: Container(
                        height: 130,
                        child: Column(
                          children: [
                            const SizedBox(
                              height: 10,
                            ),
                            TextField(
                              controller: nameController,
                              decoration: const InputDecoration(
                                hintText: "Enter the name",
                                border: OutlineInputBorder(
                                    borderRadius:
                                        BorderRadius.all(Radius.circular(10))),
                                labelText: 'Contact Name',
                              ),
                            ),
                            const SizedBox(
                              height: 10,
                            ),
                            TextField(
                              controller: numbController,
                              keyboardType: TextInputType.number,
                              decoration: const InputDecoration(
                                hintText: "enter the number",
                                border: OutlineInputBorder(
                                    borderRadius:
                                        BorderRadius.all(Radius.circular(10))),
                                labelText: 'Contact Number',
                              ),
                            )
                          ],
                        ),
                      ),
                      actions: [
                        TextButton(
                            onPressed: () {
                              // String name = nameController.text.trim();
                              // String Number = numbController.text.trim();
                              // if (name.isNotEmpty && Number.isNotEmpty) {
                              addContact();
                              // }
                            },
                            child: Text("Save")),
                      ],
                    ),
                  );
                });
          },
          label: Row(
            children: const [Icon(Icons.person_add_alt), Text("Add New")],
          )),
      body: SafeArea(
        child: ListView(
          children: [
            Container(
              margin: EdgeInsets.only(top: 10, left: 180),
              child: const Text(
                "Contact",
                style: TextStyle(fontSize: 35.5, fontWeight: FontWeight.w800),
              ),
            ),
            Container(
              child: Row(
                children: [
                  Flexible(
                      flex: 1,
                      child: Container(
                        margin: EdgeInsets.only(left: 20, right: 20),
                        child: TextField(
                          cursorColor: Colors.grey[350],
                          decoration: InputDecoration(
                            fillColor: Colors.grey[200],
                            filled: true,
                            border: OutlineInputBorder(
                                borderRadius: BorderRadius.circular(15),
                                borderSide: BorderSide.none),
                            hintText: 'Search',
                            prefixIcon: Container(
                              padding: EdgeInsets.all(15),
                              child: Icon(Icons.search),
                            ),
                          ),
                        ),
                      ))
                ],
              ),
            ),
            const Padding(
              padding: EdgeInsets.only(left: 20, top: 30),
              child: Text(
                "My Contacts()",
                style: TextStyle(fontWeight: FontWeight.bold, fontSize: 20),
              ),
            ),
            Contact.myContactList.isEmpty
                ? Container(
                    margin: const EdgeInsets.only(top: 12, left: 180),
                    child: const Text("No Contact Yet..."),
                  )
                : Expanded(
                    child: ListView.builder(
                      shrinkWrap: true,
                        itemCount: Contact.myContactList.length,
                        itemBuilder: ((context, index) {
                          return ListTile(
                            title:
                                Text("${Contact.myContactList[index]['name']}"),
                            subtitle: Text(
                                "${Contact.myContactList[index]['number']}"),
                          );
                        })),
                  ),
            // Container(
            //   margin: EdgeInsets.only(top: 12, left: 180),
            //   child: Contact.myContactList.isEmpty
            //       ? const Text(
            //           "No Contact Yet...",
            //           style: TextStyle(fontSize: 20),
            //         )
            //       : Expanded(
            //           child: ListView.builder(
            //               itemCount: Contact.myContactList.length,
            //               itemBuilder: ((context, index) {
            //                 return ListTile(
            //                   title: Text(
            //                       "${Contact.myContactList[index]['name']}"),
            //                   subtitle: Text(
            //                       "${Contact.myContactList[index]['number']}"),
            //                 );
            //               })),
            //         ),
            // )
          ],
        ),
      ),
    );
  }

  Widget getRow(index) {
    return ListTile(
      title: Text(Contact.myContactList[index]['name']),
      subtitle: Text(Contact.myContactList[index]['number']),
    );
  }
}
